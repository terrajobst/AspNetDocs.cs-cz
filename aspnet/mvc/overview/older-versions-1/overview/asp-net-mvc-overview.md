---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: ASP.NET MVC – přehled | Microsoft Docs
author: microsoft
description: Přečtěte si o rozdílech mezi aplikacemi ASP.NET MVC a aplikacemi ASP.NET Web Forms. Naučte se, jak se rozhodnout, kdy vytvořit aplikaci ASP.NET MVC.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 73965c71f37de13e3813df089a253fde528ea7ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541557"
---
# <a name="aspnet-mvc-overview"></a>Přehled rozhraní ASP.NET MVC

od [Microsoftu](https://github.com/microsoft)

> Přečtěte si o rozdílech mezi aplikacemi ASP.NET MVC a aplikacemi ASP.NET Web Forms. Naučte se, jak se rozhodnout, kdy vytvořit aplikaci ASP.NET MVC.

Architektonický vzor architektury MVC (Model-View-Controller) odděluje aplikaci na tři hlavní komponenty: model, zobrazení a kontroler. Rozhraní ASP.NET MVC poskytuje alternativu ke vzorům webových formulářů ASP.NET pro vytváření webových aplikací založených na MVC. ASP.NET MVC je jednoduchá prezentační architektura s možností intenzivního testování, která (stejně jako u aplikací webových formulářů) je integrována do stávajících funkcí technologie ASP.NET, jako jsou hlavní stránky a ověřování na základě členství. Rozhraní MVC je definováno v oboru názvů **System. Web. Mvc** a je základní podporovanou částí oboru názvů **System. Web** .   
  
MVC je standardní návrhový vzor, s nímž je obeznámena celá řada vývojářů. Pro některé typy webových aplikací bude architektura MVC výhodou. Další budou i nadále využívat tradiční vzor aplikací ASP.NET, který využívá webové formuláře a zpětná vystavení. Ostatní typy webových aplikací budou tyto dva přístupy kombinovat – vzájemně se nevylučují.   
  
Architektura MVC zahrnuje následující součásti:

[![volání akce kontroleru, která očekává hodnotu parametru.](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**Obrázek 01**: vyvolání akce kontroleru, která očekává hodnotu parametru ([kliknutím zobrazíte obrázek v plné velikosti](asp-net-mvc-overview/_static/image2.png)).

- **Modely**. Objekty modelu jsou části aplikace, které implementují logiku pro datovou doménu aplikace s. Objekty modelů často načítají a ukládají stav modelu v databázi. Objekt produktu může například načíst informace z databáze, pracovat na ní a pak zapsat aktualizované informace zpět do tabulky Products v SQL Server.

V malých aplikacích model často představuje koncepční oddělení, nikoli fyzické. Například pokud aplikace přečte sadu dat a pošle ji do zobrazení, aplikace nemá fyzickou modelovou vrstvu a přidružené třídy. V takovém případě datová sada převezme roli objektu modelu.

- **Zobrazení**. Zobrazení jsou komponenty, které zobrazují uživatelské rozhraní (UI) aplikace. Toto uživatelské rozhraní je zpravidla vytvořeno na základě dat modelu. Příkladem může být zobrazení pro úpravy tabulky Products, která zobrazuje textová pole, rozevírací seznamy a zaškrtávací políčka na základě aktuálního stavu objektu Products.

- **Řadiče**. Kontrolery jsou komponenty, které zpracovávají interakci s uživatelem, pracují s modelem a konečně vybírají vykreslené zobrazení zobrazující uživatelské rozhraní. V aplikaci MVC zobrazení pouze zobrazuje informace, zatímco kontroler zpracovává vstup uživatele a interakci s uživatelem a reaguje na ně. Například kontroler zpracovává hodnoty řetězce dotazu a předá tyto hodnoty do modelu, který pak dotazuje databázi pomocí hodnot.

Vzor MVC pomáhá vytvářet aplikace, které separují jednotlivé aspekty aplikace (logika vstupu, obchodní logika a logika uživatelského rozhraní) současně poskytují volné párování mezi těmito elementy. Vzor určuje, kde by jednotlivé typy logiky měly být v aplikaci umístěny. Logika uživatelského rozhraní patří do zobrazení. Logika vstupu patří do kontroleru. Obchodní logika patří do modelu. Tato separace pomáhá zvládnout tvorbu složitých aplikací, neboť umožňuje soustředit se v každém okamžiku pouze na jeden aspekt jejich implementace. Můžete se například soustředit na zobrazení bez závislosti na obchodní logice.   
  
Vzor MVC kromě správy složitých aplikací také v porovnání s aplikacemi technologie ASP.NET využívajícími webové formuláře usnadňuje testování aplikací. Ve webové aplikaci ASP.NET využívající webové formuláře se jedna a tatáž třída využívá k zobrazení výstupu i k reakci na vstup uživatele. Vytváření automatizovaných testů pro aplikace ASP.NET využívající webové formuláře může být složité, protože k testování jednotlivých stránek je třeba vytvořit instanci třídy stránky, všech jejích podřízených ovládacích prvků a dalších závislých tříd v aplikaci. Vzhledem k tomu, že ke spuštění stránky jsou vytvářeny instance tolika tříd, může být obtížné soustředit se výlučně na jednotlivé části aplikace. Implementace testů pro aplikace ASP.NET využívající webové formuláře proto může být obtížnější než u aplikací MVC. Testy u aplikací ASP.NET využívajících webové formuláře navíc vyžadují webový server. Architektura MVC odděluje jednotlivé komponenty a výrazně využívá rozhraní, což umožňuje testování jednotlivých komponent izolovaně od zbytku architektury.   
  
Volné párování mezi třemi hlavními komponentami architektury MVC rovněž podporuje paralelní vývoj. Například jeden vývojář může pracovat na zobrazení, druhý vývojář může pracovat s logikou kontroleru a třetí vývojář se může soustředit na obchodní logiku v modelu.

## <a name="deciding-when-to-create-an-mvc-application"></a>Rozhodnutí o tom, kdy vytvořit aplikaci MVC

Je třeba důkladně zvážit, zda webovou aplikaci implementovat pomocí architektury ASP.NET MVC nebo pomocí modelu webových formulářů technologie ASP.NET. Architektura MVC nenahrazuje model webových formulářů – pro webové aplikace lze využít oba tyto přístupy. (Stávající aplikace využívající webové formuláře budou i nadále pracovat stejným způsobem jako doposud.)   
  
Dříve než se rozhodnete, zda použít architekturu MVC nebo model webových formulářů, zvažte výhody obou těchto přístupů.

### <a name="advantages-of-an-mvc-based-web-application"></a>Výhody webové aplikace využívající architekturu MVC

Architektura ASP.NET MVC nabízí následující výhody:

- Rozdělením na model, zobrazení a kontroler usnadňuje správu složitých aplikací.
- Nevyužívá stav zobrazení ani formuláře umístěné na serveru. Z tohoto důvodu je architektura MVC ideální pro vývojáře, kteří chtějí mít plnou kontrolu nad chováním aplikace.
- Využívá vzor Front Controller, který zpracovává požadavky webové aplikace prostřednictvím jediného kontroleru. To umožňuje návrh aplikací podporujících infrastrukturu s rozsáhlým směrováním. Další informace najdete v části [front Controller](https://go.microsoft.com/fwlink/?LinkId=106357 "Front-Controller") na webu MSDN.
- Poskytuje lepší podporu pro vývoj řízený testováním (TDD).
- Funguje dobře pro webové aplikace, které jsou podporovány velkými týmy vývojářů a webovými návrháři, kteří potřebují vysoký stupeň kontroly nad chováním aplikace.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Výhody webové aplikace využívající webové formuláře

Architektura využívající webové formuláře nabízí následující výhody:

- Podporuje model událostí, který zachovává stav prostřednictvím protokolu HTTP, což je výhodné pro vývoj obchodních webových aplikací. Aplikace využívající webové formuláře poskytuje desítky událostí, které jsou podporovány stovkami ovládacích prvků serveru.
- Využívá vzor Page Controller, který přidává funkce jednotlivým stránkám. Další informace najdete v tématu [kontroler stránky](https://go.microsoft.com/fwlink/?LinkId=106359 "Kontroler stránky") na webu MSDN.
- Používá zobrazení stavů nebo serverových formulářů, které usnadňují správu informací o stavu.
- Dobře se hodí pro menší týmy webových vývojářů a návrhářů, které chtějí využít nabídky velkého množství komponent vhodných k rychlému vývoji aplikací.
- Obecně platí, že pro vývoj aplikací je méně složitá, protože komponenty (třída **stránky** , ovládací prvky atd.) jsou pevně integrované a obvykle vyžadují méně kódu než model MVC.

## <a name="features-of-the-aspnet-mvc-framework"></a>Funkce architektury ASP.NET MVC

Architektura ASP.NET MVC poskytuje následující funkce:

- Oddělení úloh aplikací (vstupní logika, obchodní logika a logika uživatelského rozhraní), testování a vývoj řízený testováním (TDD) ve výchozím nastavení. Všechny základní kontrakty architektury MVC jsou založeny na rozhraní a lze je testovat pomocí mock objektů, což jsou simulované objekty, které napodobují chování skutečných objektů v aplikaci. Můžete testovat aplikaci po jednotkách bez nutnosti spouštět kontrolery v procesu ASP.NET, takže je testování jednotek rychlé a flexibilní. Můžete použít jakékoli prostředí testování jednotek, které je kompatibilní s rozhraním .NET Framework.
- Rozšiřitelná a modulární architektura. Komponenty architektury ASP.NET MVC jsou navrženy tak, aby je bylo možné snadno nahradit a přizpůsobit. Můžete zařadit vlastní zobrazovací modul, zásady směrování adres URL, serializaci parametrů metody akce a další komponenty. Architektura ASP.NET MVC dále podporuje použití modelů kontejnerů DI (Dependency Injection) a IOC (Inversion of Control). Možnost DI umožňuje vložit objekty do třídy a nemusíte přitom spoléhat na třídu a vytvořit samotný objekt. Technologie IOC určuje, že když objekt vyžaduje jiný objekt, první objekt by měl získat druhý objekt z vnějšího zdroje, jako je konfigurační soubor. Tím je testování jednodušší.
- Výkonná součást mapování adres URL, která umožňuje vytvářet aplikace, které mají srozumitelnější a prohledávatelné adresy URL. Adresy URL nemusí obsahovat přípony souborů a jsou navrženy tak, aby podporovaly vzory mapování adres URL, které jsou vhodné k optimalizace pro vyhledávací weby (SEO) a adresování REST (representational state transfer).
- Podpora pro použití kódu značek v existujících souborech značek stránek ASP.NET (soubory .aspx), uživatelských ovládacích prvků (soubory .ascx) a hlavních stránek (soubory .master) jako šablon zobrazení. Existující funkce ASP.NET můžete použít s architekturou ASP.NET MVC, jako jsou například vnořené stránky předlohy, vložené výrazy (&lt;% =%&gt;), deklarativní serverové ovládací prvky, šablony, datové vazby, lokalizace a tak dále.
- Podpora stávajících funkcí ASP.NET. Architektura ASP.NET MVC umožňuje využívat funkce, jako je ověřování pomocí formulářů a ověřování systému Windows, autorizace adres URL, členství a role, ukládání dat a výstupu do mezipaměti, správa stavů relací a profilů, sledování stavu, konfigurace systému a architektura zprostředkovatele.

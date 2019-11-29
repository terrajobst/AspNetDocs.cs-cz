---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: Začínáme s webovými formuláři ASP.NET 4,7 a sadou Visual Studio 2017 | Microsoft Docs
author: Erikre
description: Tato série podrobných kurzů vás seznámí se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,7 a Microsoft Visual Studio
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615457"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a>Začínáme s webovými formuláři ASP.NET 4,5 a sadou Visual Studio 2017

[Stáhnout vzorový projekt Wingtip Toys (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [Stáhnout elektronickou knihu (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

V této sérii kurzů se dozvíte, jak vytvořit aplikaci webových formulářů v ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio 2017. 

## <a name="introduction"></a>Úvod

Tato série kurzů vás provede vytvořením aplikace webových formulářů ASP.NET pomocí sady Visual Studio 2017 a ASP.NET 4,5. Vytvoříte aplikaci s názvem **Wingtip Toys** – zjednodušená webová stránka prezentace prodej položek online. Během série se zvýrazní nové funkce ASP.NET 4,5.

### <a name="target-audience"></a>Cílová skupina

Pro tuto řadu kurzů jsou noví vývojáři pro ASP.NET webové formuláře cílovou skupinou.

Měli byste mít několik znalostí v následujících oblastech:

- Objektově orientované programování (OOP) a jazyky
- Vývoj pro web (HTML, CSS, JavaScript)
- Relační databáze
- N-vrstvá architektura

Pokud si chcete projít tyto oblasti, vezměte v úvahu následující obsah:

- [Začínáme pomocí vizuáluC#](https://msdn.microsoft.com/library/a72418yk.aspx)
- [Vývoj pro web](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, php, jQuery](http://w3schools.com/)
- [Relační databáze](http://en.wikipedia.org/wiki/Relational_database)
- [Vícevrstvá architektura](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a>Funkce aplikace

Mezi funkce webového formuláře ASP.NET prezentované v tomto seriálu patří:

- Projekt webové aplikace (ne web projektu)
- Webové formuláře
- Stránky předlohy, konfigurace
- Spouštěcí rutina
- Entity Framework Code First, LocalDB
- Žádost o ověření
- Datové ovládací prvky silného typu
- Vazba modelu
- Datové poznámky
- Zprostředkovatelé hodnot
- SSL a OAuth
- ASP.NET Identity, konfigurace a autorizace
- Nenáročná ověření
- Směrování
- Zpracování chyb v ASP.NET

### <a name="application-scenarios-and-tasks"></a>Scénáře a úlohy aplikací

Úkoly řady kurzů zahrnují:

- Vytvoření, kontrola a spuštění nového projektu
- Vytvoření struktury databáze
- Inicializace a osazení databáze
- Přizpůsobení uživatelského rozhraní pomocí stylů, grafiky a stránky předlohy
- Přidávání stránek a navigace
- Zobrazení podrobností nabídky a dat produktu
- Vytvoření nákupního košíku
- Přidání podpory SSL a OAuth
- Přidání způsobu platby
- Zahrnutí role správce a uživatele do aplikace
- Omezení přístupu ke konkrétním stránkám a složce
- Nahrání souboru do webové aplikace
- Implementace ověřování vstupu
- Registrace tras pro webovou aplikaci
- Implementace zpracování chyb a protokolování chyb

## <a name="overview"></a>Přehled

Tato série kurzů je určená pro někoho, kdo se seznámí s koncepty programování, ale novinkou pro ASP.NET webové formuláře. Pokud jste již obeznámeni s webovými formuláři ASP.NET, může vám tato řada stále pomáhat s novými funkcemi ASP.NET 4,5. Pro čtenáře, kteří nejsou obeznámeni s koncepty programování a ASP.NET webovými formuláři, si přečtěte další kurzy webových formulářů, které jsou k dispozici v části [Začínáme](../../../index.md) na webu ASP.NET.

ASP.NET 4,5 poskytnutý v této sérii kurzů obsahuje následující funkce:

- Jednoduché uživatelské rozhraní pro vytváření projektů, které nabízí [podporu pro řadu ASP.NETch platforem](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (webové formuláře, MVC a webové rozhraní API).
- [Zavedení](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), rozložení, vytváření a reakce rozhraní návrhu.
- [ASP.NET identity](../../../../identity/index.md)nový systém členství v ASP.NET, který funguje stejně ve všech ASP.NET architekturách a pracuje s jiným softwarem pro hostování webů, než je služba IIS.
- [Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx)

  Aktualizace Entity Framework, která vám umožní:
  - Načtení a manipulace s daty jako objekty silného typu
  - Asynchronní přístup k datům
  - Zpracování přechodných chyb připojení
  - Log SQL – příkazy

Úplný seznam funkcí ASP.NET 4,5 najdete v tématu [ASP.NET and Web Tools pro Visual Studio 2013 poznámky k verzi](../../../../visual-studio/overview/2013/release-notes.md).

### <a name="the-wingtip-toys-sample-application"></a>Ukázková aplikace Wingtip Toys

Následující snímky obrazovky jsou z aplikace webových formulářů ASP.NET, kterou vytvoříte v této sérii kurzů. Při spuštění aplikace v aplikaci Visual Studio se zobrazí následující Domovská stránka webu.

![Wingtip Toys – výchozí stránka](introduction-and-overview/_static/image1.png)

Můžete se zaregistrovat jako nový uživatel nebo se přihlásit jako stávající uživatel. Horní navigace obsahuje odkazy na kategorie produktů a jejich produkty z databáze.

Pokud vyberete možnost **produkty**, zobrazí se všechny dostupné produkty. 

![Společnost Wingtip Toys – produkty](introduction-and-overview/_static/image2.png)

Pokud vyberete určitý produkt, zobrazí se podrobnosti o produktu.

![Společnost Wingtip Toys – podrobnosti o produktu](introduction-and-overview/_static/image3.png)

Jako uživatel můžete registrovat a přihlašovat se pomocí výchozích funkcí šablon webových formulářů. Tento kurz taky vysvětluje, jak se přihlašovat pomocí existujícího účtu Gmail. Kromě toho se můžete přihlásit jako správce a přidat nebo odebrat produkty z databáze.

![Wingtip Toys – přihlášení](introduction-and-overview/_static/image4.png)

Jakmile se přihlásíte jako uživatel, můžete přidat produkty do nákupního košíku a zaregistrovat se pomocí služby PayPal. Ukázková aplikace je navržená tak, aby fungovala v izolovaném prostoru pro vývojáře ve službě PayPal. Žádná skutečná peněžní transakce se neuskuteční.

![Wingtip Toys – nákupní košík](introduction-and-overview/_static/image5.png)

PayPal potvrdí informace o vašem účtu, objednávce a platbě.

![Wingtip Toys – PayPal](introduction-and-overview/_static/image6.png)

Po návratu ze služby PayPal můžete zkontrolovat a dokončit vaši objednávku.

![Wingtip Toys – revize objednávky](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a>Požadavky

Než začnete, ujistěte se, že je v počítači nainstalovaný následující software:

- [Microsoft Visual Studio 2017 nebo Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).

.NET Framework se nainstaluje automaticky.

Tato série kurzů používá Microsoft Visual Studio Community 2017. K dokončení této série kurzů můžete použít buď to, nebo Microsoft Visual Studio 2017.

Všimněte si následujících informací o aplikaci Visual Studio:

* Microsoft Visual Studio 2017 a Microsoft Visual Studio Community 2017 se v této sérii kurzů označují jako *Visual Studio* .

* Visual Studio 2017 je nainstalováno vedle všech starších verzí, které jsou již nainstalovány. Weby vytvořené v dřívějších verzích lze otevřít v aplikaci Visual Studio 2017 a nadále otevírat v předchozích verzích.

* Při prvním spuštění sady Visual Studio se předpokládá, že jste vybrali nastavení *vývoje webu* . Další informace najdete v tématu [Postupy: výběr nastavení prostředí pro vývoj webu](https://msdn.microsoft.com/library/ff521558.aspx).

Po instalaci požadovaných součástí jste připraveni začít vytvářet webový projekt prezentovaný v této sérii kurzů.

## <a name="download-the-sample-application"></a>Stažení ukázkové aplikace

 Dokončenou ukázkovou aplikaci si můžete kdykoli stáhnout z webu ukázek na webu MSDN:

[Začínáme s webovými formuláři ASP.NET 4,5 a Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 

 Tento soubor ke stažení obsahuje následující položky:

- Ukázková aplikace ve složce *WingtipToys*
- Prostředky použité k vytvoření ukázkové aplikace ve složce *WingtipToys-assets* ve složce *WingtipToys*

Soubor ke stažení je soubor *. zip* . Pokud chcete zobrazit dokončený projekt, který tato série kurzů vytvoří, najděte a *C#* vyberte složku v souboru. zip. Uložte C# složku do složky, kterou používáte pro práci s projekty aplikace Visual Studio. Ve výchozím nastavení je složka projektů sady Visual Studio 2017:

<strong>C:\Users&#92;</strong>  <strong><em>&lt;username&gt;</em></strong> <strong>\source\repos</strong>

Přejmenujte ***C#*** složku na ***WingtipToys***.

> [!NOTE]
> Pokud ve složce Projects již máte složku s názvem *WingtipToys* , před přejmenováním *C#* složky na *WingtipToys*tuto existující složku dočasně přejmenujte.

Chcete-li spustit dokončený projekt, otevřete složku *WingtipToys* a dvakrát klikněte na soubor *WingtipToys. sln* . Visual Studio 2017 otevře projekt. Potom klikněte pravým tlačítkem myši na soubor *Default. aspx* v **Průzkumník řešení** a vyberte možnost **Zobrazit v prohlížeči**.

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a>Vytvoření kvízu webových formulářů ASP.NET pro kontrolu obsahu

Po dokončení série kurzů si požádejte kvíz o testování znalostí a posílení klíčových konceptů. Každá otázka obsahuje vysvětlení a odkazy na další doprovodné materiály.

* [Kvíz webových formulářů ASP.NET](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a>Kurzová podpora a komentáře

V případě otázek a komentářů použijte část Q a část, která je součástí [Začínáme s webovými formuláři ASP.NET 4,5 a Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) s ukázkovou stránkou.

Komentáře k této sérii kurzů jsou Vítá vás. Po aktualizaci této série kurzů se provede každé úsilí, aby se zohlednily opravy nebo návrhy na vylepšení.

Pokud dojde k chybě, mohou být příslušné chybové zprávy matoucí, a to bez vhodného vysvětlení, jak je opravit. Nápovědu můžete vyhledat ve [fórech ASP.NET](https://forums.asp.net/). Dalším dobrým zdrojem je oddíl Q a a ve [Začínáme s webovými formuláři ASP.NET 4,5 a na ukázkové stránce Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#). 

> [!div class="step-by-step"]
> [Next](create-the-project.md)

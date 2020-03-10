---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
title: Vytvořit projekt | Microsoft Docs
author: Erikre
description: V této sérii kurzů se seznámíte se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro My...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 2ce36f78-8ecb-4ab1-b748-6d0ab633ea3f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
msc.type: authoredcontent
ms.openlocfilehash: 62918b17f42e54dfe4e45a08927b1039dcbb7012
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78571986"
---
# <a name="create-the-project"></a>Vytvoření projektu

od [Erik Reitan](https://github.com/Erikre)

[Stáhnout vzorový projekt Wingtip Toys (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [Stáhnout elektronickou knihu (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> V této sérii kurzů se naučíte základy vytváření webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro web. K dispozici je Visual Studio 2013 [projekt se C# zdrojovým kódem](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) , který se doprovází v této sérii kurzů.

V tomto kurzu vytvoříte, zkontrolujete a spustíte výchozí projekt v aplikaci Visual Studio, který vám umožní seznámit se s funkcemi ASP.NET. Prohlédněte si také prostředí sady Visual Studio.

## <a name="what-youll-learn"></a>Naučíte se:

- Vytvoření nového projektu webových formulářů.
- Struktura souborů projektu webových formulářů.
- Jak spustit projekt v aplikaci Visual Studio.
- Různé funkce výchozí aplikace webových formulářů.
- Některé základy použití prostředí sady Visual Studio.

## <a name="creating-the-project"></a>Vytvoření projektu

1. Otevřete sadu Visual Studio.
2. V nabídce **soubor** v aplikaci Visual Studio vyberte **Nový projekt** . 

    ![Vytvořit projekt – položka nabídky nový projekt](create-the-project/_static/image1.png)
3. Na levé straně vyberte **šablony** -&gt; skupinu **Web** Templates &gt; **Visual C#**  -.
4. V prostředním sloupci vyberte šablonu **webové aplikace ASP.NET** .  
 Tato série kurzů používá .NET Framework 4.5.2.
5. Pojmenujte projekt *WingtipToys* a klikněte na tlačítko **OK** . 

    ![Dialogové okno vytvořit projekt – nový projekt](create-the-project/_static/image2.png)

    > [!NOTE]
    > Název projektu v této sérii kurzů je **WingtipToys**. Doporučuje se použít tento *přesný* název projektu, aby kód poskytnutý v rámci řady kurzů fungoval podle očekávání.

6. Klikněte na tlačítko **Změna ověřování**. Vyberte **jednotlivé uživatelské účty** a klikněte na tlačítko **OK** .

7. Vyberte šablonu **webové formuláře** a klikněte na tlačítko **OK** .

    ![Vytvořit projekt – nová šablona projektu](create-the-project/_static/image3.png)

Vytvoření projektu bude trvat trochu dlouho. Až to bude připravené, otevřete stránku **Default. aspx** .

![Vytvořit projekt – nová šablona projektu](create-the-project/_static/image4.png)

Můžete přepínat mezi **návrhovým** zobrazením a zobrazením **zdrojového kódu** výběrem možnosti v dolní části středu okna. **Návrhové** zobrazení zobrazuje ASP.NET webové stránky, stránky předlohy, stránky obsahu, stránky HTML a uživatelské ovládací prvky pomocí zobrazení blízko-WYSIWYG. Zobrazení **zdroje** zobrazuje značku HTML pro vaši webovou stránku, kterou můžete upravovat.

> [!TIP] 
> 
> **Principy ASP.NET Framework**
> 
> Webové formuláře ASP.NET umožňují vytvářet dynamické weby pomocí známého modelu založeného na událostech a přetahování. Návrhová plocha a stovky ovládacích prvků a komponent vám umožní rychle vytvořit sofistikované a výkonné weby na základě uživatelského rozhraní s přístupem k datům. Úložiště Wingtip Toys je založené na ASP.NET webových formulářích, ale mnoho konceptů, které se v této sérii kurzů naučíte, platí pro všechny ASP.NET.
> 
> ASP.NET nabízí čtyři primární vývojové architektury:
> 
> - [Webové formuláře ASP.NET](../../../index.md)  
>  Rozhraní webového formuláře cílí na vývojáře, kteří dávají přednost deklarativnímu a řídicímu programování, jako je například Microsoft model Windows Forms (WinForms) a WPF/XAML/Silverlight. Nabízí model vývoje řízený návrhářem WYSIWYG, takže je oblíbený s vývojáři, kteří hledají prostředí pro vývoj webů s rychlým vývojem aplikací (RAD). Pokud s webovým programováním začínáte a jste obeznámeni s tradičními nástroji Microsoft RAD Client Development Tools (například pro Visual Basic a C#vizuál), můžete rychle vytvořit webovou aplikaci, aniž byste měli zkušenosti s HTML a JavaScriptem.
> - [ASP.NET MVC](../../../../mvc/index.md)  
>  ASP.NET MVC cílí na vývojáře, kteří mají zájem o vzory a principy, jako je vývoj řízený testy, oddělení obav, inverze řídicích prvků (IoC) a vkládání závislostí (DI). Toto rozhraní podporuje oddělení vrstvy obchodní logiky webové aplikace od své prezentační vrstvy.
> - [Webové stránky ASP.NET](../../../../web-pages/index.md)  
>  Webové stránky ASP.NET cílí na vývojáře, kteří chtějí jednoduchý příběh pro vývoj na webu, a to na řádcích PHP. V modelu webové stránky vytvoříte stránky HTML a pak na stránku přidáte kód založený na serveru, aby bylo možné dynamicky řídit, jak se tento kód vykresluje. Webové stránky jsou specificky navržené jako odlehčené rozhraní a je to nejjednodušší vstupní bod do ASP.NET pro lidi, kteří znají kód HTML, ale nemusí mít k dispozici široké vývojové prostředí – například students nebo nadšence. Pro webové vývojáře, kteří znají PHP nebo podobná rozhraní, je také dobrým způsobem, jak začít používat ASP.NET.
> - [ASP.NET aplikace s jednou stránkou](../../../../single-page-application/index.md)  
>  ASP.NET aplikace (SPA) pomáhá sestavovat aplikace, které zahrnují významné interakce na straně klienta, pomocí HTML 5, šablon stylů CSS 3 a JavaScriptu. Aktualizace ASP.NET and Web Tools 2012,2 je dodávána s novou šablonou pro vytváření aplikací s jedním stránkou pomocí webového rozhraní vyseknutí. js a ASP.NET. Kromě nové šablony zabezpečeného hesla (SPA) jsou k dispozici také nové šablony zabezpečeného hesla vytvořené komunitou ke stažení.
> 
> Kromě čtyř hlavních vývojových platforem ASP.NET také nabízí další technologie, které jsou důležité pro znalosti a zkušenosti s nimi, ale nejsou zahrnuté v této sérii kurzů:
> 
> - [Webové rozhraní API pro ASP.NET](../../../../web-api/index.md) – rozhraní pro vytváření služeb HTTP, které dosahují široké škály klientů, včetně prohlížečů a mobilních zařízení.
> - [ASP.NET Signal](../../../../signalr/index.md) – knihovna, která usnadňuje vývoj webové funkce v reálném čase.

### <a name="reviewing-the-project"></a>Kontrola projektu

V aplikaci Visual Studio umožňuje okno **Průzkumník řešení** spravovat soubory projektu. Pojďme se podívat na složky, které byly přidány do aplikace v **Průzkumník řešení**. Šablona webové aplikace přidá základní strukturu složek:

![Vytvoření projektu – Průzkumník řešení](create-the-project/_static/image5.png)

Visual Studio vytvoří některé počáteční složky a soubory pro váš projekt. První soubory, s kterými budete pracovat později v tomto kurzu, jsou následující:

| **File** | **Účel** |
| --- | --- |
| *Default. aspx* | Obvykle se první stránka zobrazuje při spuštění aplikace v prohlížeči. |
| *Lokalita. Master* | Stránka, která umožňuje vytvořit konzistentní rozložení a používat standardní chování pro stránky v aplikaci. |
| *Global. asax* | Volitelný soubor, který obsahuje kód pro reagování na události na úrovni aplikace a na úrovni relace vyvolané moduly HTTP ASP.NET nebo. |
| *Web. config* | Konfigurační data pro aplikaci. |

### <a name="running-the-default-web-application"></a>Spuštění výchozí webové aplikace

Výchozí webová aplikace poskytuje bohatou zkušenost na základě integrovaných funkcí a podpory. Bez jakýchkoli změn v výchozích projektech webových formulářů je aplikace připravená ke spuštění v místním webovém prohlížeči.

1. Při práci v aplikaci Visual Studio stiskněte klávesu ***F5*** .   
 Aplikace se sestaví a zobrazí ve webovém prohlížeči.  

    ![Vytvořit projekt – výchozí stránka](create-the-project/_static/image6.png)
2. Jakmile dokončíte kontrolu běžící aplikace, zavřete okno prohlížeče.

V této výchozí webové aplikaci jsou tři hlavní stránky: *Default. aspx* (Home), *About. aspx*a *Contact. aspx*. Každá z těchto stránek se dá získat z horního navigačního panelu. Ve složce účtu jsou k dispozici také dvě další stránky, které jsou obsaženy na stránce Register. aspx a login. aspx. Tyto dvě stránky umožňují používat možnosti členství ASP.NET k vytváření, ukládání a ověřování uživatelských přihlašovacích údajů.

## <a name="aspnet-web-forms-background"></a>Pozadí webových formulářů ASP.NET

Webové formuláře ASP.NET jsou stránky, které jsou založené na Microsoft ASP.NET technologiích, ve kterých kód, který běží na serveru, dynamicky generuje výstup webové stránky do prohlížeče nebo klientského zařízení. Stránka webových formulářů ASP.NET automaticky vykreslí správné soubory HTML kompatibilní s prohlížečem pro funkce, jako jsou styly, rozložení a tak dále. Webové formuláře jsou kompatibilní s jakýmkoli jazykem podporovaným modulem CLR (Common Language Runtime) .NET, jako je například C#Microsoft Visual Basic a Microsoft Visual. Webové formuláře jsou také postavené na [.NET Framework Microsoftu](https://msdn.microsoft.com/vstudio/aa496123), které poskytují výhody, jako je spravované prostředí, bezpečnost typů a dědičnost.

Při spuštění stránky webových formulářů ASP.NET se stránka prochází životním cyklem, ve kterém provádí řadu kroků zpracování. Tyto kroky zahrnují inicializaci, vytváření instancí ovládacích prvků, obnovení a udržování stavu, spuštění kódu obslužné rutiny události a vykreslování. Vzhledem k tomu, že jste obeznámeni s výkonem webových formulářů ASP.NET, je důležité, abyste porozuměli [životnímu cyklu ASP.NET stránky](https://msdn.microsoft.com/library/ms178472(v=vs.100).aspx) , abyste mohli psát kód do příslušné fáze životního cyklu pro efekt, který máte v úmyslu.

Když webový server obdrží požadavek na stránku, vyhledá stránku, zpracuje ji, odešle ji do prohlížeče a pak zahodí všechny informace o stránce. Pokud uživatel znovu vyžádá stejnou stránku, server zopakuje celou sekvenci a znovu zpracuje stránku od začátku. Jiný způsob je, že server nemá žádnou paměť stránek, které zpracoval – stránky jsou bezstavové. Rozhraní stránky ASP.NET automaticky zpracovává úlohu udržování stavu vaší stránky a jejích ovládacích prvků a poskytuje explicitní způsoby udržování stavu informací specifických pro aplikaci.

> [!TIP] 
> 
> **Funkce webové aplikace v šabloně webové formuláře aplikace**
> 
> Šablona aplikace webových formulářů ASP.NET poskytuje bohatou sadu integrovaných funkcí. Neposkytuje vám jenom stránku *Home. aspx* , stránku *About. aspx* , stránku *Contact. aspx* , ale taky obsahuje funkce členství, které registrují uživatele a ukládají jejich přihlašovací údaje, aby se mohli přihlásit k webu. Tento přehled obsahuje další informace o některých funkcích obsažených v šabloně aplikace webových formulářů ASP.NET a o tom, jak se používají v aplikaci Wingtip Toys.
> 
> **Členství**
> 
> [ASP.NET](https://msdn.microsoft.com/library/yh26yfzy.aspx) Identita ukládá přihlašovací údaje vašich uživatelů do databáze vytvořené aplikací. Když se uživatelé přihlásí, aplikace ověří své přihlašovací údaje čtením databáze. Složka *účtu* vašeho projektu obsahuje soubory, které implementují různé části členství: registrace, přihlášení, změna hesla a autorizace přístupu. Webové formuláře ASP.NET navíc podporují OAuth a OpenID. Tato vylepšení ověřování umožňují uživatelům přihlašovat se k webu pomocí stávajících přihlašovacích údajů, z těchto účtů jako Facebook, Twitter, Windows Live a Google.
> 
> ![Vytvoření projektu – Průzkumník řešení (ASP.NET Identity)](create-the-project/_static/image7.png)
> 
> Ve výchozím nastavení šablona vytvoří databázi členství pomocí výchozího názvu databáze na instanci SQL Server Express LocalDB, server pro vývoj databáze, který je součástí Visual Studio Express 2013 pro web.
> 
> **SQL Server Express LocalDB**
> 
> [SQL Server Express LocalDB](https://technet.microsoft.com/library/hh510202.aspx) je zjednodušená verze SQL Server, která má mnoho funkcí programovatelnosti databáze SQL Server. SQL Server Express LocalDB běží v uživatelském režimu a má rychlou a nulovou instalaci s konfigurací, která má krátký seznam požadovaných součástí instalace. V Microsoft SQL Server lze jakékoli databáze nebo kód Transact-SQL přesunout z SQL Server Express LocalDB na SQL Server a SQL Azure bez kroků upgradu. Proto je možné SQL Server Express LocalDB použít jako vývojářské prostředí pro aplikace cílené na všechny edice SQL Server. SQL Server Express LocalDB umožňuje funkce, jako jsou uložené procedury, uživatelsky definované funkce a agregace, .NET Framework integraci, prostorové typy a další, které nejsou v SQL Server Compact k dispozici.
> 
> **Stránky předlohy**
> 
> [Stránka předlohy ASP.NET](https://msdn.microsoft.com/library/wtxbf3hh.aspx) definuje konzistentní vzhled a chování pro všechny stránky ve vaší aplikaci. Rozložení stránky předlohy se sloučí s obsahem z jednotlivé stránky obsahu, aby se vytvořila poslední stránka, kterou uživatel uvidí. V aplikaci Wingtip Toys upravíte stránku *site. Master* , aby všechny stránky na webu Wingtip Toys sdílely stejné logo a navigační panel.
> 
> **HTML5**
> 
> Šablona aplikace webových formulářů ASP.NET podporuje [HTML5](http://www.w3schools.com/html/html5_intro.asp), což je nejnovější verze jazyka značek HTML. HTML5 podporuje nové prvky a funkce, které usnadňují vytváření webů.
> 
> **Modernizr**
> 
> Pro prohlížeče, které nepodporují HTML5, můžete použít [modernizr](http://www.modernizr.com/). Modernizr je open source knihovna JavaScriptu, která dokáže zjistit, jestli prohlížeč podporuje funkce HTML5, a povolit je, pokud ne. V šabloně aplikace webových formulářů ASP.NET se modernizr nainstaluje jako balíček NuGet.
> 
> **Bootstrap**
> 
> Šablony projektu Visual Studio 2013 používají [bootstrap](http://getbootstrap.com/), rozložení a rozhraní pro vytváření na Twitteru. Bootstrap používá CSS3 k tomu, aby poskytovala reagující návrh, což znamená, že rozložení se můžou dynamicky přizpůsobovat různým velikostem oken prohlížeče. Můžete také použít funkci zaváděcí rutiny Bootstrap, která umožňuje snadno změnit vzhled a chování aplikace. Ve výchozím nastavení Šablona webové aplikace ASP.NET v Visual Studio 2013 zahrnuje Bootstrap jako balíček NuGet.
> 
> **Balíčky NuGet**
> 
> Šablona aplikace webových formulářů ASP.NET zahrnuje sadu balíčků [NuGet](http://www.nuget.org/) . Tyto balíčky poskytují komponentní funkce ve formě Open Source knihoven a nástrojů. Existuje široká škála balíčků, které vám pomůžou vytvářet a testovat vaše aplikace. Visual Studio umožňuje snadno přidávat, odebírat a aktualizovat balíčky NuGet. Vývojáři můžou vytvářet a přidávat balíčky taky do NuGet.
> 
> ![Vytvoření projektu – dialogové okno NuGet](create-the-project/_static/image8.png)
> 
> Při instalaci balíčku nástroje NuGet kopíruje soubory do vašeho řešení a automaticky provede libovolné změny, například přidání odkazů a změna konfigurace přidružené k vaší webové aplikaci. Pokud se rozhodnete tuto knihovnu odebrat, NuGet odebere soubory a vrátí zpět všechny změny provedené v projektu, aby nezůstaly žádné zbytečné soubory. NuGet je k dispozici v nabídce **nástroje** v aplikaci Visual Studio.
> 
> **jQuery**
> 
> [jQuery](http://jquery.com/) je rychlá a Stručná knihovna JavaScriptu, která zjednodušuje procházení dokumentů HTML, zpracování událostí, animace a interakce AJAX pro rychlý vývoj na webu. Knihovna jQuery JavaScript je obsažena v šabloně aplikace webových formulářů ASP.NET jako balíček NuGet.
> 
> **Nenáročná ověření**
> 
> Předdefinované ovládací prvky pro ověřování jsou nakonfigurovány tak, aby používaly nenápadný jazyk JavaScript pro logiku ověřování na straně klienta. To významně snižuje množství vykreslování JavaScriptu vloženého do značek stránky a zmenšuje celkovou velikost stránky. Nenápadní ověřování je globálně přidáno do šablony aplikace webových formulářů ASP.NET na základě nastavení v elementu &lt;appSettings&gt; souboru *Web. config* v kořenovém adresáři aplikace.
> 
> **Entity Framework Code First**
> 
> Kromě funkcí v šabloně aplikace webových formulářů ASP.NET používá aplikace Wingtip Toys [Code First Entity Framework](https://weblogs.asp.net/scottgu/archive/2010/12/08/announcing-entity-framework-code-first-ctp5-release.aspx), což je knihovna NuGet, která umožňuje vývoj orientovaný na kód při práci s daty. Jednoduše řečeno, vytvoří databázovou část vaší aplikace za vás, a to na základě kódu, který píšete. Pomocí Entity Framework načtete a manipulujete s daty jako s objekty silného typu. To vám umožní soustředit se na obchodní logiku ve vaší aplikaci, a ne na podrobnosti o způsobu, jakým jsou data dostupná.
> 
> Další informace o nainstalovaných knihovnách a balíčcích, které jsou součástí šablony webových formulářů ASP.NET, najdete v seznamu nainstalovaných balíčků NuGet. Chcete-li to provést, v aplikaci Visual Studio vytvořte nový projekt webových formulářů, vyberte **nástroje** > **správce balíčků NuGet** > **Spravovat balíčky NuGet pro řešení**a vyberte **nainstalované balíčky** v dialogovém okně **Spravovat balíčky NuGet** .

### <a name="touring-visual-studio"></a>Prohlídka sady Visual Studio

Primární okna v sadě Visual Studio zahrnují **Průzkumník řešení**, **Průzkumník serveru** (**Průzkumník databáze** v aplikaci Express), **okno Vlastnosti** **, panel nástrojů,** **panel nástrojů**a **okno dokumentu**.

![Vytvoření projektu – dialogové okno NuGet](create-the-project/_static/image9.png)

Další informace o aplikaci Visual Studio naleznete v tématu [vizuální průvodce pro Visual Web Developer](https://msdn.microsoft.com/library/ee410104.aspx).

## <a name="summary"></a>Souhrn

V tomto kurzu jste vytvořili, zkontrolovali a spustili výchozí aplikaci webových formulářů. Zkontrolovali jste různé funkce výchozí webové formuláře a zjistili jsme základy použití prostředí sady Visual Studio. V následujících kurzech vytvoříte vrstvu přístupu k datům.

## <a name="additional-resources"></a>Další prostředky

[Výběr správného programovacího modelu](../../../videos/how-do-i/choosing-the-right-programming-model.md)   
[Projekty webové aplikace versus webové projekty](https://msdn.microsoft.com/library/dd547590.aspx)   
[Přehled stránek webových formulářů ASP.NET](https://msdn.microsoft.com/library/428509ah.aspx)

> [!div class="step-by-step"]
> [Předchozí](introduction-and-overview.md)
> [Další](create_the_data_access_layer.md)

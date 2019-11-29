---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: Vytvoření aplikace Movie Database za 15 minut s ASP.NET MVC (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther sestaví celou databázi založenou na ASP.NET aplikaci MVC od začátku do konce. Tento kurz je skvělým úvodem pro lidi, kteří jsou noví t...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ce8161d29a8ab4005e2b20462b08c9e10ee815a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595427"
---
# <a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a>Vytvoření aplikace Movie Database za 15 minut s ASP.NET MVC (VB)

od [Stephen Walther](https://github.com/StephenWalther)

[Stáhnout kód](https://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> Stephen Walther sestaví celou databázi založenou na ASP.NET aplikaci MVC od začátku do konce. Tento kurz je skvělým úvodem pro lidi, kteří jsou noví v architektuře ASP.NET MVC a chtějí získat představu o procesu vytváření ASP.NET aplikace MVC.

Účelem tohoto kurzu je poskytnout představu o tom, co je třeba, aby se vytvořila aplikace ASP.NET MVC. V tomto kurzu jsem procházím sestavením celé aplikace ASP.NET MVC od začátku do konce. Ukážeme vám, jak vytvořit jednoduchou aplikaci založenou na databázích, která ukazuje, jak můžete vytvářet a upravovat záznamy databáze.

Abychom zjednodušili proces sestavení naší aplikace, využijte výhod funkcí pro generování uživatelského rozhraní sady Visual Studio 2008. Visual Studio vám umožní vygenerovat počáteční kód a obsah pro naše řadiče, modely a zobrazení.

Pokud jste pracovali s Active Server stránkami nebo ASP.NET, měli byste najít ASP.NET MVC velmi dobře. Zobrazení ASP.NET MVC jsou velmi podobná stránkám v aplikaci Active Server Pages. A stejně jako tradiční aplikace webových formulářů v ASP.NET poskytuje ASP.NET MVC úplný přístup k bohatě dostupnému sadě jazyků a tříd poskytovaných rozhraním .NET Framework.

Doufám, že v tomto kurzu získáte představu o tom, jak se bude prostředí sestavování aplikace ASP.NET MVC podobná i odlišná než při vytváření Active Server stránek nebo ASP.NET webových formulářů.

## <a name="overview-of-the-movie-database-application"></a>Přehled aplikace Movie Database

Vzhledem k tomu, že naším cílem je udržet věci jednoduché, vytvoříme velmi jednoduchou aplikaci filmové databáze. Naše jednoduchá aplikace pro video databáze nám umožní provést tři věci:

1. Výpis sady záznamů filmové databáze
2. Vytvoří nový záznam filmové databáze.
3. Upravit existující záznam filmové databáze

A to proto, že chceme zachovat věci jednoduché, využijeme minimální počet funkcí rozhraní ASP.NET MVC, které je potřeba k sestavení naší aplikace. Nebudete například používat vývoj řízený testováním.

Aby bylo možné vytvořit naši aplikaci, je nutné provést následující kroky:

1. Vytvoření projektu webové aplikace ASP.NET MVC
2. Vytvoření databáze
3. Vytvoření databázového modelu
4. Vytvoření kontroleru ASP.NET MVC
5. Vytvoření zobrazení ASP.NET MVC

## <a name="preliminaries"></a>Nezbytné úkony

K vytvoření aplikace ASP.NET MVC budete potřebovat Visual Studio 2008 nebo Visual Web Developer 2008 Express. Také je nutné stáhnout architekturu ASP.NET MVC.

Pokud nevlastníte sadu Visual Studio 2008, můžete si stáhnout zkušební verzi sady Visual 2008 Studio 90 dne na tomto webu:

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

Alternativně můžete vytvářet aplikace ASP.NET MVC pomocí nástroje Visual Web Developer Express 2008. Pokud se rozhodnete použít Visual Web Developer Express, je nutné mít nainstalovanou aktualizaci Service Pack 1. Visual Web Developer 2008 Express s aktualizací Service Pack 1 si můžete stáhnout z tohoto webu:

[https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;d isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

Po instalaci sady Visual Studio 2008 nebo Visual Web Developer 2008 je nutné nainstalovat rozhraní ASP.NET MVC. Rozhraní ASP.NET MVC si můžete stáhnout z následujícího webu:

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> Místo toho, aby se ASP.NET Framework a rozhraní ASP.NET MVC nestáhly samostatně, můžete využít výhod instalace webové platformy. Instalace webové platformy je aplikace, která umožňuje snadnou správu nainstalovaných aplikací v počítači:
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)

## <a name="creating-an-aspnet-mvc-web-application-project"></a>Vytvoření projektu webové aplikace ASP.NET MVC

Pojďme začít vytvořením nového projektu webové aplikace ASP.NET MVC v aplikaci Visual Studio 2008. Vyberte soubor možnosti nabídky **, nový projekt** a zobrazí se dialogové okno Nový projekt na obrázku 1. Jako programovací jazyk vyberte Visual Basic a vyberte šablonu projektu webové aplikace ASP.NET MVC. Pojmenujte projekt MovieApp a klikněte na tlačítko OK.

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)

**Obrázek 01**: dialogové okno Nový projekt ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))

Ujistěte se, že jste vybrali .NET Framework 3,5 z rozevíracího seznamu v horní části dialogového okna Nový projekt nebo když se neobjeví šablona projektu webové aplikace ASP.NET MVC.

Pokaždé, když vytvoříte nový projekt webové aplikace MVC, Visual Studio vás vyzve k vytvoření samostatného projektu testování částí. Zobrazí se dialogové okno na obrázku 2. Vzhledem k tomu, že v tomto kurzu nebudeme vytvářet testy kvůli časovým omezením (a Ano, máme to trochu dopustili), vyberte možnost **ne** a klikněte na tlačítko **OK** .

> [!NOTE] 
> 
> Visual Web Developer nepodporuje projekty testů.

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)

**Obrázek 02**: dialogové okno vytvořit projekt testování částí ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))

Aplikace ASP.NET MVC má standardní sadu složek: modely, zobrazení a složky řadičů. Tuto standardní sadu složek můžete zobrazit v okně Průzkumník řešení. Aby bylo možné sestavit aplikaci filmové databáze, bude nutné přidat soubory do každého z modelů, zobrazení a složek řadičů.

Při vytváření nové aplikace MVC se sadou Visual Studio získáte ukázkovou aplikaci. Vzhledem k tomu, že chceme začít od začátku, musíme obsah pro tuto ukázkovou aplikaci odstranit. Je nutné odstranit následující soubor a následující složku:

- Controllers\HomeController.vb
- Views\Home

## <a name="creating-the-database"></a>Vytvoření databáze

Musíme vytvořit databázi pro ukládání záznamů filmové databáze. Donovanovo, Visual Studio obsahuje bezplatnou databázi s názvem SQL Server Express. Pomocí těchto kroků vytvořte databázi:

1. V okně Průzkumník řešení klikněte pravým tlačítkem na složku data\_aplikace a vyberte možnost nabídky **Přidat, nová položka**.
2. Vyberte kategorii **dat** a vyberte šablonu **databáze SQL Server** (viz obrázek 3).
3. Pojmenujte novou databázi *MoviesDB. mdf* a klikněte na tlačítko **Přidat** .

Po vytvoření databáze se můžete připojit k databázi dvojitým kliknutím na soubor MoviesDB. mdf umístěný ve složce App\_data. Dvojím kliknutím na soubor MoviesDB. mdf se otevře okno Průzkumník serveru.

> [!NOTE] 
> 
> Okno Průzkumník serveru se jmenuje okno Průzkumník databáze v případě aplikace Visual Web Developer.

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)

**Obrázek 03**: vytvoření databáze Microsoft SQL Server ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))

Dál je potřeba vytvořit novou databázovou tabulku. V okně Průzkumníka serveru klikněte pravým tlačítkem na složku tabulky a vyberte možnost nabídky **Přidat novou tabulku**. Když vyberete tuto možnost nabídky, otevře se Návrhář tabulky databáze. Vytvořte následující databázové sloupce:

<a id="0.2_table01"></a>

| **Název sloupce** | **Datový typ** | **Povoluje hodnoty null.** |
| --- | --- | --- |
| Id | Hmot | Nepravda |
| Název | Nvarchar (100) | Nepravda |
| Adresářů | Nvarchar (100) | Nepravda |
| DateReleased | Datum a čas | Nepravda |

První sloupec, sloupec ID, má dvě speciální vlastnosti. Nejprve je třeba označit sloupec ID jako sloupec primárního klíče. Po výběru sloupce ID klikněte na tlačítko **nastavit primární klíč** (je to ikona, která vypadá jako klíč). Za druhé je třeba označit sloupec ID jako sloupec identity. Ve sloupci okno Vlastnosti přejděte dolů k části specifikace identity a rozbalte ji. Změňte vlastnost **is identity** na hodnotu **Yes**. Až budete hotovi, tabulka by měla vypadat jako na obrázku 4.

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)

**Obrázek 04**: tabulka video ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))

Posledním krokem je uložení nové tabulky. Klikněte na tlačítko Uložit (ikona disketové jednotky) a dejte nové tabulce Název filmy.

Po dokončení vytváření tabulky přidejte do tabulky některé filmové záznamy. V okně Průzkumník serveru klikněte pravým tlačítkem myši na tabulku filmy a vyberte možnost nabídky **Zobrazit data tabulky**. Zadejte seznam oblíbených filmů (viz obrázek 5).

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)

**Obrázek 05**: zadání filmových záznamů ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))

## <a name="creating-the-model"></a>Vytvoření modelu

Dál je potřeba vytvořit sadu tříd, které reprezentují naši databázi. Musíme vytvořit model databáze. Využijeme Microsoft Entity Framework k automatickému vygenerování tříd pro náš databázový model.

> [!NOTE] 
> 
> Rozhraní ASP.NET MVC není vázané na Microsoft Entity Framework. Třídy databázového modelu můžete vytvořit pomocí různých nástrojů pro mapování relačních objektů (nebo M), včetně LINQ to SQL, antisonic a NHibernate.

Pomocí těchto kroků spusťte Průvodce model EDM (Entity Data Model):

1. V okně Průzkumník řešení klikněte pravým tlačítkem na složku modely a vyberte možnost nabídky **Přidat, nová položka**.
2. Vyberte kategorii **dat** a vyberte šablonu **model EDM (Entity Data Model) ADO.NET** .
3. Udělte datovému modelu název *MoviesDBModel. edmx* a klikněte na tlačítko **Přidat** .

Po kliknutí na tlačítko Přidat se zobrazí průvodce model EDM (Entity Data Model) (viz obrázek 6). Pomocí těchto kroků dokončete Průvodce:

1. V kroku **zvolit obsah modelu** vyberte možnost **Generovat z databáze** .
2. V kroku **Vybrat datové připojení** použijte datové připojení *MoviesDB. mdf* a název *MoviesDBEntities* pro nastavení připojení. Klikněte na tlačítko **Další** .
3. V kroku **Zvolte databázové objekty** rozbalte uzel tabulky a vyberte tabulku filmy. Zadejte obor názvů *MovieApp. Models* a klikněte na tlačítko **Dokončit** .

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)

**Obrázek 6**: generování databázového modelu pomocí Průvodce model EDM (Entity Data Model) ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))

Po dokončení průvodce model EDM (Entity Data Model) se otevře Návrhář model EDM (Entity Data Model). Návrhář by měl zobrazit tabulku databáze filmů (viz obrázek 7).

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)

**Obrázek 07**: Návrhář model EDM (Entity Data Model) ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))

Než budeme pokračovat, musíme udělat jednu změnu. Průvodce data entity vygeneruje třídu modelu s názvem filmy, která představuje tabulku databáze filmů. Vzhledem k tomu, že použijeme třídu filmů k reprezentování konkrétního filmu, musíme upravit název třídy tak, aby se místo *filmů* použil *film* (číslo v čísle místo plural).

Dvakrát klikněte na název třídy na návrhové ploše a změňte název třídy z filmů na film. Po provedení této změny klikněte na tlačítko **Uložit** (ikona disketové jednotky) a vygenerujte třídu video.

## <a name="creating-the-aspnet-mvc-controller"></a>Vytváří se kontroler ASP.NET MVC.

Dalším krokem je vytvoření kontroleru ASP.NET MVC. Kontroler zodpovídá za řízení způsobu interakce uživatele s aplikací ASP.NET MVC.

Postupujte podle těchto kroků:

1. V okně Průzkumník řešení klikněte pravým tlačítkem na složku řadiče a vyberte možnost nabídky **Přidat, kontroler**.
2. V dialogovém okně Přidat řadič zadejte název *HomeController* a zaškrtněte políčko **přidat metody akcí pro scénáře vytváření, aktualizace a podrobností** (viz obrázek 8).
3. Kliknutím na tlačítko **Přidat** přidejte nový kontroler do projektu.

Po dokončení těchto kroků se vytvoří kontroler v seznamu 1. Všimněte si, že obsahuje metody pojmenované index, Details, Create a Edit. V následujících částech přidáme potřebný kód pro získání těchto metod, které budou fungovat.

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)

**Obrázek 08**: Přidání nového KONTROLERU ASP.NET MVC ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))

**Výpis 1 – Controllers\HomeController.vb**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a>Výpis záznamů databáze

Metoda index () domovského kontroleru je výchozí metodou pro aplikaci ASP.NET MVC. Při spuštění aplikace ASP.NET MVC je metoda index () první volanou metodou řadiče.

K zobrazení seznamu záznamů z tabulky databáze filmů použijeme metodu index (). Budeme využívat třídy databázového modelu, které jsme vytvořili dříve k načtení záznamů filmové databáze pomocí metody index ().

Změnil (a) jsem třídu HomeController v seznamu 2 tak, že obsahuje nové soukromé pole s názvem \_DB. Třída MoviesDBEntities představuje náš databázový model a my tuto třídu používá ke komunikaci s naší databází.

Také jsem změnil () metodu index () v seznamu 2. Metoda index () používá třídu MoviesDBEntities k načtení všech záznamů filmů z tabulky databáze filmů. Výraz *\_DB. MovieSet. ToList – ()* vrátí seznam všech filmových záznamů z tabulky databáze filmů.

Seznam videí se předává do zobrazení. Cokoli, co se předává metodě View (), se do zobrazení předává jako data zobrazení.

**Výpis 2 – Controllers/HomeController. vb (upravená metoda indexu)**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

Metoda index () vrací zobrazení s názvem index. Pro zobrazení seznamu záznamů o filmových databázích je potřeba toto zobrazení vytvořit. Postupujte podle těchto kroků:

Před otevřením dialogového okna **Přidat zobrazení** nebo v rozevíracím seznamu **Třída zobrazení dat** by se měly sestavit projekt (vyberte možnost nabídky **sestavit, sestavit řešení**).

1. Klikněte pravým tlačítkem myši na metodu index () v editoru kódu a vyberte možnost nabídky **Přidat zobrazení** (viz obrázek 9).
2. V dialogovém okně Přidat zobrazení ověřte, že je zaškrtnuté políčko **vytvořit zobrazení silného typu** .
3. V rozevíracím seznamu **Zobrazit obsah** vyberte *seznam*hodnot.
4. V rozevíracím seznamu **Třída zobrazení dat** vyberte hodnotu *MovieApp. video*.
5. Kliknutím na tlačítko Přidat vytvoříte nové zobrazení (viz obrázek 10).

Po dokončení těchto kroků se do složky Views\Home přidá nové zobrazení s názvem index. aspx. Obsah zobrazení index je obsažen v seznamu 3.

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)

**Obrázek 09**: Přidání zobrazení z akce kontroleru ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)

**Obrázek 10**: vytvoření nového zobrazení pomocí dialogového okna Přidat zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

V zobrazení index se zobrazí všechny záznamy filmů z tabulky databáze filmů v tabulce HTML. Zobrazení obsahuje pro každou smyčku, která projde jednotlivými filmy reprezentovanými vlastností ViewData. model. Pokud spustíte aplikaci stisknutím klávesy F5, zobrazí se webová stránka na obrázku 11.

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)

**Obrázek 11**: Zobrazení indexu ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))

## <a name="creating-new-database-records"></a>Vytváření nových záznamů databáze

Zobrazení indexu, které jsme vytvořili v předchozí části, obsahuje odkaz pro vytváření nových záznamů databáze. Pojďme dopředu a implementovat logiku a vytvořit zobrazení nezbytné pro vytváření nových záznamů filmové databáze.

Domovský kontroler obsahuje dvě metody nazvané Create (). První metoda Create () nemá žádné parametry. Toto přetížení metody Create () slouží k zobrazení HTML formuláře pro vytvoření nového záznamu filmové databáze.

Druhá metoda Create () má parametr FormCollection. Toto přetížení metody Create () je voláno, když je formulář HTML pro vytvoření nového filmu odeslán na server. Všimněte si, že tato druhá metoda Create () má atribut AcceptVerbs, který brání volání metody, pokud není provedena operace HTTP POST.

Tato druhá metoda Create () byla upravena v aktualizované třídě HomeController v seznamu 4. Nová verze metody Create () akceptuje parametr videa a obsahuje logiku pro vložení nového videa do tabulky databáze filmů.

> [!NOTE] 
> 
> Všimněte si atributu BIND. Vzhledem k tomu, že nechci aktualizovat vlastnost ID filmu z formuláře HTML, musíme tuto vlastnost explicitně vyloučit.

**Výpis 4 – Controllers\HomeController.vb (upravená metoda Create)**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

Visual Studio usnadňuje vytvoření formuláře pro vytvoření nového záznamu filmové databáze (viz obrázek 12). Postupujte podle těchto kroků:

1. Klikněte pravým tlačítkem myši na metodu Create () v editoru kódu a vyberte možnost nabídky **Přidat zobrazení**.
2. Ověřte, jestli je zaškrtnuté políčko **vytvořit zobrazení silného typu** .
3. V rozevíracím seznamu **Zobrazit obsah** vyberte hodnotu *vytvořit*.
4. V rozevíracím seznamu **Třída zobrazení dat** vyberte hodnotu *MovieApp. video*.
5. Kliknutím na tlačítko **Přidat** vytvoříte nové zobrazení.

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)

**Obrázek 12**: Přidání zobrazení pro vytvoření ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))

Visual Studio vygeneruje zobrazení v seznamu 5 automaticky. Toto zobrazení obsahuje formulář HTML, který obsahuje pole, která odpovídají jednotlivým vlastnostem třídy video.

**Výpis 5 – Views\Home\Create.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> Formulář HTML generovaný dialogem přidat zobrazení vygeneruje pole ID formuláře. Vzhledem k tomu, že sloupec ID je sloupec identity, nepotřebujeme toto pole formuláře a můžete ho bezpečně odebrat.

Po přidání zobrazení vytvořit můžete do databáze přidat nové záznamy filmů. Spusťte aplikaci stisknutím klávesy F5 a kliknutím na odkaz vytvořit nový zobrazte formulář na obrázku 13. Pokud dokončíte a odešlete formulář, vytvoří se nový záznam filmové databáze.

Všimněte si, že se automaticky vyřadí ověření formuláře. Pokud zapomenete zadat datum vydání pro film nebo zadáte neplatné datum vydání, bude formulář znovu zobrazen a pole Datum vydání bude zvýrazněno.

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)

**Obrázek 13**: vytvoření nového záznamu filmové databáze ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))

## <a name="editing-existing-database-records"></a>Úprava stávajících záznamů databáze

V předchozích částech jsme probrali, jak můžete vypsat a vytvořit nové záznamy databáze. V této poslední části probereme, jak můžete upravit existující záznamy databáze.

Nejdřív musíme vygenerovat formulář pro úpravy. Tento krok je snadný, protože Visual Studio vygeneruje automaticky formulář pro úpravy pro nás. Otevřete třídu HomeController. vb v editoru kódu sady Visual Studio a postupujte podle následujících kroků:

1. Klikněte pravým tlačítkem myši na metodu Edit () v editoru kódu a vyberte možnost nabídky **Přidat zobrazení** (viz obrázek 14).
2. Zaškrtněte políčko s názvem **vytvořit zobrazení silného typu**.
3. V rozevíracím seznamu **Zobrazit obsah** vyberte *Upravit*hodnotu.
4. V rozevíracím seznamu **Třída zobrazení dat** vyberte hodnotu *MovieApp. video*.
5. Kliknutím na tlačítko **Přidat** vytvoříte nové zobrazení.

Po dokončení těchto kroků se přidá nové zobrazení s názvem Edit. aspx do složky Views\Home. Toto zobrazení obsahuje formulář HTML pro úpravu záznamu filmu.

[![dialogového okna Nový projekt](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)

**Obrázek 14**: Přidání zobrazení pro úpravy ([kliknutím zobrazíte obrázek v plné velikosti](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))

> [!NOTE] 
> 
> Zobrazení pro úpravy obsahuje pole formuláře HTML, které odpovídá vlastnosti ID videa. Vzhledem k tomu, že nechcete, aby uživatelé upravovali hodnotu vlastnosti ID, měli byste toto pole formuláře odebrat.

Nakonec musíme upravit domovský kontroler tak, aby podporoval úpravu záznamu databáze. Aktualizovaná třída HomeController je obsažena v seznamu 6.

**Výpis 6 – Controllers\HomeController.vb (upravit metody)**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

V výpisu 6 jsem přidali další logiku k přetížení obou metod Edit (). První metoda Edit () vrátí záznam filmové databáze, který odpovídá parametru ID předanému metodě. Druhé přetížení provede aktualizace záznamu filmu v databázi.

Všimněte si, že je nutné načíst původní film, a pak volat ApplyPropertyChanges (), chcete-li aktualizovat existující film v databázi.

## <a name="summary"></a>Přehled

Účelem tohoto kurzu je poskytnout představu o zkušenostech s vytvářením aplikace ASP.NET MVC. Doufám, že se vám zjistilo, že vytvoření webové aplikace ASP.NET MVC je velmi podobné prostředí pro vytváření Active Serverch stránek nebo ASP.NET aplikace.

V tomto kurzu jsme prozkoumali jenom základní funkce architektury ASP.NET MVC. V budoucích kurzech podrobně hlubší témata, jako jsou například řadiče, akce kontroleru, zobrazení, zobrazení dat a pomocníky HTML.

> [!div class="step-by-step"]
> [Předchozí](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)

---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: 'Iterace #1 – Vytvoření aplikace (VB) | Microsoft Docs'
author: microsoft
description: 'V první iteraci vytvoříme nejjednodušším způsobem správce kontaktů. Přidáváme podporu základních databázových operací: vytvořit, číst, aktualizovat a D...'
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: c6bf4712fb734cf14420fd62c9eaf190a2c28168
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602317"
---
# <a name="iteration-1--create-the-application-vb"></a>Iterace #1 – Vytvoření aplikace (VB)

od [Microsoftu](https://github.com/microsoft)

[Stáhnout kód](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> V první iteraci vytvoříme nejjednodušším způsobem správce kontaktů. Přidáváme podporu základních databázových operací: vytváření, čtení, aktualizace a odstraňování (CRUD).

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Sestavování aplikace MVC pro správu kontaktů ASP.NET (VB)

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

V této první iteraci sestavíme základní aplikaci. Cílem je sestavovat správce kontaktů co nejrychleji a nejjednodušším způsobem. V pozdějších iteracích Vylepšete návrh aplikace.

Aplikace Správce kontaktů je základní aplikace řízená databázemi. Aplikaci můžete použít k vytvoření nových kontaktů, úpravám existujících kontaktů a odstraňování kontaktů.

V této iteraci provedeme následující kroky:

1. Aplikace ASP.NET MVC
2. Vytvoření databáze pro uložení kontaktů
3. Vygenerujte třídu modelu pro naši databázi pomocí Microsoft Entity Framework
4. Umožňuje vytvořit akci a zobrazení kontroleru, které nám umožní zobrazit seznam všech kontaktů v databázi.
5. Vytvoření akcí kontroleru a zobrazení, které nám umožňuje vytvořit nový kontakt v databázi
6. Vytvoření akcí kontroleru a zobrazení, které nám umožňuje upravit existující kontakt v databázi
7. Vytvoření akcí kontroleru a zobrazení, které nám umožňuje odstranit existující kontakt v databázi

## <a name="software-prerequisites"></a>Požadavky na software

V aplikacích ASP.NET MVC musíte mít v počítači nainstalován buď sadu Visual Studio 2008 nebo Visual Web Developer 2008 (Visual Web Developer je bezplatná verze sady Visual Studio, která neobsahuje všechny pokročilé funkce sady Visual Studio). Zkušební verzi sady Visual Studio 2008 nebo Visual Web Developer si můžete stáhnout z následující adresy:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> Pro ASP.NET aplikace MVC s Visual Web Developer musíte mít nainstalovanou sadu Visual Web Developer Service Pack 1. Bez aktualizace Service Pack 1 nemůžete vytvářet projekty webových aplikací.

ASP.NET MVC Framework Rozhraní ASP.NET MVC si můžete stáhnout z následující adresy:

[https://www.asp.net/mvc](../../../index.md)

V tomto kurzu použijeme Microsoft Entity Framework pro přístup k databázi. Entity Framework je součástí .NET Framework 3,5 Service Pack 1. Tuto aktualizaci Service Pack si můžete stáhnout z následujícího umístění:

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;d isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

Jako alternativu k provedení každého z těchto stažení můžete využít instalaci webové platformy (Web PI). Web PI si můžete stáhnout z následující adresy:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>Projekt MVC ASP.NET

Projekt webové aplikace ASP.NET MVC Spusťte Visual Studio a vyberte soubor možnosti nabídky **, nový projekt**. Zobrazí se dialogové okno **Nový projekt** (viz obrázek 1). Vyberte typ **webového** projektu a šablonu **webové aplikace ASP.NET MVC** . Pojmenujte nový projekt *ContactManager* a klikněte na tlačítko OK.

Ujistěte se, že jste vybrali .NET Framework 3,5 v rozevíracím seznamu v pravém horním rohu dialogového okna **Nový projekt** . V opačném případě se šablona webové aplikace ASP.NET MVC nezobrazí.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)

**Obrázek 01**: dialogové okno Nový projekt ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image2.png))

Aplikace ASP.NET MVC, zobrazí se dialogové okno **vytvořit projekt testování částí** . Pomocí tohoto dialogového okna můžete označit, že chcete vytvořit a přidat projekt testu jednotek k řešení při vytváření aplikace ASP.NET MVC. I když v této iteraci nebudeme vytvářet testy jednotek, měli byste vybrat možnost **Ano, vytvořit projekt testování částí,** protože plánujeme přidat testy jednotek v pozdější iteraci. Přidání testovacího projektu při prvním vytvoření nového projektu ASP.NET MVC je mnohem snazší než přidání testovacího projektu po vytvoření projektu ASP.NET MVC.

> [!NOTE] 
> 
> Vzhledem k tomu, že Visual Web Developer nepodporuje testovací projekty, nezískáte dialogové okno vytvořit projekt testování částí při použití aplikace Visual Web Developer.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)

**Obrázek 02**: dialogové okno vytvořit projekt testování částí ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image4.png))

Aplikace ASP.NET MVC se zobrazí v okně Visual Studio Průzkumník řešení (viz obrázek 3). Pokud nevidíte Průzkumník řešení okno, můžete toto okno otevřít tak, že vyberete zobrazení možnosti nabídky **, Průzkumník řešení**. Všimněte si, že řešení obsahuje dva projekty: projekt MVC ASP.NET a projekt testů. Projekt ASP.NET MVC má název ContactManager a testovací projekt má název ContactManager. Tests.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)

**Obrázek 03**: okno Průzkumník řešení ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image6.png))

## <a name="deleting-the-project-sample-files"></a>Odstraňují se ukázkové soubory projektu.

Šablona projektu ASP.NET MVC obsahuje ukázkové soubory pro řadiče a zobrazení. Před vytvořením nové aplikace ASP.NET MVC byste tyto soubory měli odstranit. Soubory a složky můžete v okně Průzkumník řešení odstranit tak, že kliknete pravým tlačítkem na soubor nebo složku a vyberete možnost nabídky **Odstranit**.

V projektu ASP.NET MVC je nutné odstranit následující soubory:

- \Controllers\HomeController.vb

- \Views\Home\About.aspx

- \Views\Home\Index.aspx

A, je nutné odstranit následující soubor z testovacího projektu:

\Controllers\HomeControllerTest.vb

## <a name="creating-the-database"></a>Vytvoření databáze

Aplikace Správce kontaktů je webová aplikace řízená databází. K uložení kontaktních informací používáme databázi.

Rozhraní ASP.NET MVC se všemi moderními databázemi, včetně Microsoft SQL Server, Oracle, MySQL a databází IBM DB2. V tomto kurzu používáme databázi Microsoft SQL Server. Při instalaci sady Visual Studio máte k dispozici možnost instalace Microsoft SQL Server Express, což je bezplatná verze databáze Microsoft SQL Server.

Vytvořte novou databázi tak, že kliknete pravým tlačítkem na složku aplikace\_data v okně Průzkumník řešení a vyberete možnost nabídka **Přidat, nová položka**. V dialogovém okně **Přidat novou položku** vyberte kategorii **dat** a šablonu **SQL Server databáze** (viz obrázek 4). Pojmenujte novou databázi ContactManagerDB. mdf a klikněte na tlačítko OK.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)

**Obrázek 04**: vytvoření nové databáze Microsoft SQL Server Express ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image8.png))

Po vytvoření nové databáze se databáze zobrazí ve složce App\_data v okně Průzkumník řešení. Dvojím kliknutím na soubor ContactManager. mdf otevřete okno Průzkumník serveru a připojte se k databázi.

> [!NOTE] 
> 
> Okno Průzkumník serveru se nazývá okno Průzkumník databáze v případě aplikace Microsoft Visual Web Developer.

Okno Průzkumník serveru můžete použít k vytvoření nových databázových objektů, například tabulek databáze, zobrazení, triggerů a uložených procedur. Klikněte pravým tlačítkem na složku tabulky a vyberte možnost nabídky **Přidat novou tabulku**. Zobrazí se Návrhář tabulky databáze (viz obrázek 5).

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)

**Obrázek 05**: Návrhář databázové tabulky ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image10.png))

Musíme vytvořit tabulku, která obsahuje následující sloupce:

<a id="0.2_table01"></a>

| **Název sloupce** | **Datový typ** | **Povoluje hodnoty null.** |
| --- | --- | --- |
| ID | int | false (nepravda) |
| FirstName | nvarchar (50) | false (nepravda) |
| LastName | nvarchar (50) | false (nepravda) |
| Telefon | nvarchar (50) | false (nepravda) |
| Email | nvarchar (255) | false (nepravda) |

První sloupec, sloupec ID, je speciální. Sloupec ID je třeba označit jako sloupec identity a sloupec primárního klíče. Označíte, že sloupec je sloupec identity rozbalením vlastností sloupce (podívejte se na dolní část obrázku 6) a posuňte se dolů na vlastnost specifikace identity. Vlastnost **(je identita)** nastavte na hodnotu **Ano**.

Sloupec označíte jako sloupec primárního klíče, a to tak, že vyberete sloupec a kliknete na tlačítko s ikonou klíče. Když je sloupec označený jako sloupec primárního klíče, zobrazí se vedle sloupce ikona klíče (viz obrázek 6).

Po dokončení vytváření tabulky klikněte na tlačítko Uložit (tlačítko s ikonou "disketa") a uložte novou tabulku. Dejte nové tabulce název *Kontakty*.

Po dokončení vytváření tabulky kontaktů databáze byste měli do tabulky přidat nějaké záznamy. V okně Průzkumník serveru klikněte pravým tlačítkem myši na tabulku Contacts (kontakty) a vyberte možnost nabídky **Zobrazit data tabulky**. Do mřížky, která se zobrazí, zadejte jeden nebo více kontaktů.

## <a name="creating-the-data-model"></a>Vytvoření datového modelu

Aplikace ASP.NET MVC se skládá z modelů, zobrazení a řadičů. Začneme vytvořením třídy modelu, která představuje tabulku kontaktů, kterou jsme vytvořili v předchozí části.

V tomto kurzu použijeme Microsoft Entity Framework k vygenerování třídy modelu z databáze automaticky.

> [!NOTE] 
> 
> Rozhraní ASP.NET MVC není nijak vázané na Microsoft Entity Framework. ASP.NET MVC můžete použít s alternativními technologiemi přístupu k databázi, včetně NHibernate, LINQ to SQL nebo ADO.NET.

Pomocí těchto kroků vytvořte třídy datového modelu:

1. V okně Průzkumník řešení klikněte pravým tlačítkem na složku modely a vyberte **Přidat, nová položka**. Zobrazí se dialogové okno **Přidat novou položku** (viz obrázek 6).
2. Vyberte kategorii **dat** a šablonu **model EDM (Entity Data Model) ADO.NET** . Pojmenujte datový model *ContactManagerModel. edmx* a klikněte na tlačítko **Přidat** . Zobrazí se Průvodce model EDM (Entity Data Model) (viz obrázek 7).
3. V kroku **zvolit obsah modelu** vyberte možnost **Generovat z databáze** (viz obrázek 7).
4. V kroku **Zvolte datové připojení** vyberte databázi ContactManagerDB. mdf a jako nastavení připojení entity zadejte název *ContactManagerDBEntities* (viz obrázek 8).
5. V kroku **Zvolte objekty databáze** zaškrtněte políčko označené tabulky (viz obrázek 9). Datový model bude obsahovat všechny tabulky obsažené v databázi (je tu jen jedna tabulka kontaktů). Zadejte *modely*oboru názvů. Průvodce dokončíte kliknutím na tlačítko Dokončit.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)

**Obrázek 6**: dialogové okno Přidat novou položku ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image12.png))

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)

**Obrázek 07**: volba obsahu modelu ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image14.png))

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)

**Obrázek 08**: Vyberte datové připojení ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image16.png)).

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)

**Obrázek 09**: volba databázových objektů ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image18.png))

Po dokončení průvodce model EDM (Entity Data Model) se zobrazí Návrhář model EDM (Entity Data Model). Návrhář zobrazí třídu, která odpovídá každé modelované tabulce. Měla by se zobrazit jedna třída s názvem kontakty.

Průvodce model EDM (Entity Data Model) generuje názvy tříd na základě názvů databázových tabulek. Skoro vždycky potřebujete změnit název třídy generované průvodcem. Klikněte pravým tlačítkem myši na třídu Contacts v návrháři a vyberte možnost nabídky **Přejmenovat**. Změňte název třídy z Contacts (plural) na kontakt (v jednotném čísle). Po změně názvu třídy by se měla třída zobrazit jako obrázek 10.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)

**Obrázek 10**: třída Contact ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image20.png))

V tuto chvíli jsme vytvořili model databáze. Třídu Contact můžeme použít k reprezentaci konkrétního záznamu kontaktu v naší databázi.

## <a name="creating-the-home-controller"></a>Vytvoření domovského kontroleru

Dalším krokem je vytvoření našeho domovského kontroleru. Domovský kontroler je výchozí řadič vyvolaný v aplikaci ASP.NET MVC.

Vytvořte třídu domovského kontroleru kliknutím pravým tlačítkem myši na složku Controllers v okně Průzkumník řešení a výběrem možnosti nabídky **Přidat, kontroler** (viz obrázek 11). Všimněte si políčka s popisem **metod přidání akcí pro scénáře vytváření, aktualizace a podrobností**. Ujistěte se, že je toto políčko zaškrtnuto před kliknutím na tlačítko **Přidat** .

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)

**Obrázek 11**: Přidání domovského kontroleru ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image22.png))

Při vytváření domovského kontroleru získáte třídu v seznamu 1.

**Výpis 1 – Controllers\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a>Výpis kontaktů

Aby bylo možné zobrazit záznamy v tabulce databáze kontaktů, musíme vytvořit akci index () a zobrazení indexu.

Adaptér Home již obsahuje akci indexu (). Musíme tuto metodu upravit tak, aby vypadala jako v seznamu 2.

**Výpis 2 – Controllers\HomeController.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

Všimněte si, že třída domovského kontroleru v seznamu 2 obsahuje soukromé pole s názvem \_entity. Pole \_entity představuje entity z datového modelu. Pole \_entit používáme ke komunikaci s databází.

Metoda index () vrací zobrazení, které představuje všechny kontakty z tabulky databáze Contacts. Výraz \_entit. ContactSet. ToList – () vrátí seznam kontaktů jako obecný seznam.

Teď, když jsme vytvořili řadič indexu, dál je potřeba vytvořit zobrazení indexu. Před vytvořením zobrazení indexu zkompilujte aplikaci výběrem možnosti nabídky **sestavení, řešení sestavení**. Projekt byste měli před přidáním zobrazení vždycky zkompilovat, aby se seznam tříd modelů zobrazoval v dialogovém okně **Přidat zobrazení** .

Zobrazení index vytvoříte tak, že kliknete pravým tlačítkem na metodu index () a vyberete možnost nabídky **Přidat zobrazení** (viz obrázek 12). Po výběru této možnosti nabídky se otevře dialogové okno **Přidat zobrazení** (viz obrázek 13).

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)

**Obrázek 12**: Přidání zobrazení indexu ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image24.png))

V dialogovém okně **Přidat zobrazení** zaškrtněte políčko **vytvořit zobrazení silného typu**. Vyberte třídu zobrazení dat ContactManager. Contact a seznam obsahu zobrazení. Výběrem těchto možností se vytvoří zobrazení, které zobrazí seznam záznamů kontaktů.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)

**Obrázek 13**: dialogové okno Přidat zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image26.png))

Po kliknutí na tlačítko **Přidat** se vygeneruje zobrazení index v seznamu 3. Všimněte si direktivy &lt;% @ Page%&gt;, která se zobrazí v horní části souboru. Zobrazení index dědí z ViewPage&lt;IEnumerable&lt;ContactManager. Models. Contact&gt;&gt; třídy. Jinými slovy, třída modelu v zobrazení představuje seznam entit kontaktů.

Tělo zobrazení indexu obsahuje smyčku foreach, která prochází každý z kontaktů reprezentovaných třídou modelu. Hodnota každé vlastnosti třídy Contact se zobrazí v tabulce HTML.

**Výpis 3-Views\Home\Index.aspx (beze změny)**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

Musíme v zobrazení indexu udělat jednu změnu. Vzhledem k tomu, že Nevytváříme zobrazení podrobností, můžeme odebrat odkaz Podrobnosti. Vyhledejte a odeberte následující kód z zobrazení index:

{. ID = položka. ID})%&gt;

Po úpravě zobrazení indexu můžete spustit aplikaci Správce kontaktů. Vyberte možnost nabídky ladění, spustit ladění nebo jednoduše stiskněte klávesu F5. Při prvním spuštění aplikace se zobrazí dialogové okno na obrázku 14. Vyberte možnost **Upravit soubor Web. config pro povolení ladění** a klikněte na tlačítko OK.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)

**Obrázek 14**: povolení ladění ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image28.png))

Ve výchozím nastavení je vráceno zobrazení index. Toto zobrazení uvádí všechna data z tabulky databáze Contacts (viz obrázek 15).

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)

**Obrázek 15**: Zobrazení indexu ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image30.png))

Všimněte si, že zobrazení indexů obsahuje odkaz s označením vytvořit nový ve spodní části zobrazení. V další části se dozvíte, jak vytvořit nové kontakty.

## <a name="creating-new-contacts"></a>Vytváření nových kontaktů

Abychom uživatelům umožnili vytvářet nové kontakty, musíme do domovského kontroleru přidat dvě akce vytvoření (). Potřebujeme vytvořit jednu akci vytvoření (), která vrátí formulář HTML pro vytvoření nového kontaktu. Musíme vytvořit druhou akci vytvoření (), která provede vlastní vložení nového kontaktu do databáze.

Nové metody Create (), které je třeba přidat do domovského kontroleru, jsou obsaženy v seznamu 4.

**Výpis 4 – Controllers\HomeController.vb (s metodami Create)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

Metodu First Create () lze vyvolat pomocí protokolu HTTP GET, zatímco druhá metoda Create () může být vyvolána pouze pomocí HTTP POST. Jinými slovy, druhá metoda Create () může být vyvolána pouze při publikování formuláře HTML. První metoda Create () jednoduše vrátí zobrazení, které obsahuje formulář HTML pro vytvoření nového kontaktu. Druhá metoda Create () je mnohem zajímavá: Přidá nový kontakt do databáze.

Všimněte si, že druhá metoda Create () byla změněna tak, aby přijímala instanci třídy Contact. Hodnoty formuláře publikované z formuláře HTML jsou vázány na tuto třídu kontaktů pomocí architektury ASP.NET MVC automaticky. Každé pole formuláře z formuláře pro vytvoření HTML je přiřazeno k vlastnosti parametru kontaktu.

Všimněte si, že parametr Contact je upraven pomocí atributu [BIND]. Atribut [BIND] je použit k vyloučení vlastnosti kontaktu s ID z vazby. Vzhledem k tomu, že vlastnost ID představuje vlastnost identity, nebudeme chtít nastavit vlastnost ID.

V těle metody Create () Entity Framework slouží k vložení nového kontaktu do databáze. Nový kontakt se přidá do existující sady kontaktů a metoda SaveChanges () se zavolá, aby se tyto změny nastavily zpátky do podkladové databáze.

Formulář HTML pro vytváření nových kontaktů můžete vygenerovat tak, že kliknete pravým tlačítkem myši na jednu z těchto dvou metod Create () a vyberete možnost nabídky **Přidat zobrazení** (viz obrázek 16).

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)

**Obrázek 16**: Přidání zobrazení pro vytvoření ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image32.png))

V dialogovém okně **Přidat zobrazení** vyberte třídu **ContactManager. Contact** a možnost **vytvořit** pro zobrazení obsahu (viz obrázek 17). Když kliknete na tlačítko **Přidat** , zobrazení pro vytvoření se vygeneruje automaticky.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)

**Obrázek 17**: zobrazení rozbalené stránky ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image34.png))

Zobrazení vytvořit obsahuje pole formuláře pro každou z vlastností třídy kontakt. Kód pro zobrazení pro vytváření je obsažen v seznamu 5.

**Výpis 5 – Views\Home\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

Po úpravě metod Create () a přidání zobrazení pro vytvoření můžete spustit aplikaci kontaktů a vytvořit nové kontakty. Kliknutím na odkaz **vytvořit nový** , který se zobrazí v zobrazení index, přejděte k zobrazení vytvořit. Zobrazení by se mělo zobrazit na obrázku 18.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)

**Obrázek 18**: zobrazení pro vytvoření ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image36.png))

## <a name="editing-contacts"></a>Úprava kontaktů

Přidání funkce pro úpravu záznamu kontaktů je velmi podobné jako přidání funkce pro vytváření nových záznamů kontaktů. Nejdřív musíme přidat dvě nové metody úprav do třídy pro domovský kontrolér. Tyto nové metody Edit () jsou obsaženy v seznamu 6.

**Výpis 6 – Controllers\HomeController.vb (s metodami úprav)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

První metoda Edit () je vyvolána operací HTTP GET. Do této metody se předává parametr ID, který představuje ID upravovaného záznamu kontaktu. Entity Framework slouží k načtení kontaktu, který odpovídá ID. Vrátí se zobrazení, které obsahuje formulář HTML pro úpravu záznamu.

Druhá metoda Edit () provede skutečnou aktualizaci databáze. Tato metoda přijímá instanci třídy Contact jako parametr. Rozhraní ASP.NET MVC váže pole formuláře z formuláře pro úpravy k této třídě automaticky. Všimněte si, že při úpravě kontaktu nezahrnete atribut [BIND] (potřebujeme hodnotu vlastnosti ID).

Entity Framework slouží k uložení upraveného kontaktu do databáze. Původní kontakt musí být nejprve načten z databáze. Dále je volána metoda Entity Framework ApplyPropertyChanges (), která zaznamená změny kontaktu. Nakonec se zavolá metoda Entity Framework SaveChanges (), aby se zachovaly změny v podkladové databázi.

Zobrazení, které obsahuje formulář pro úpravy, můžete vygenerovat kliknutím pravým tlačítkem myši na metodu Edit () a výběrem možnosti nabídky přidat zobrazení. V dialogovém okně Přidat zobrazení vyberte třídu **ContactManager. Models. Contact** a obsah zobrazení pro **Úpravy** (viz obrázek 19).

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)

**Obrázek 19**: Přidání zobrazení pro úpravy ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image38.png))

Když kliknete na tlačítko Přidat, automaticky se vygeneruje nové zobrazení pro úpravy. Generovaný formulář HTML obsahuje pole, která odpovídají jednotlivým vlastnostem třídy kontaktů (viz výpis 7).

**Výpis 7 – Views\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>Odstraňování kontaktů

Chcete-li odstranit kontakty, je nutné přidat dvě akce odstranění () do třídy řadiče pro domácí zařízení. První akce Odstranit () zobrazí formulář pro potvrzení odstranění. Druhá akce Odstranit () provede skutečné odstranění.

> [!NOTE] 
> 
> Později v případě iterace #7 změníme manažera kontaktů tak, aby podporovala jeden krok AJAX DELETE.

Dvě nové metody Delete () jsou obsaženy v seznamu 8.

**Výpis 8-Controllers\HomeController.vb (metody Delete)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

První metoda Delete () vrátí potvrzovací formulář pro odstranění záznamu kontaktu z databáze (viz Figure20). Druhá metoda Delete () provede z databáze skutečnou operaci odstranění. Po načtení původního kontaktu z databáze jsou volána metody Entity Framework OdstranitObjekt () a SaveChanges () k provedení odstranění databáze.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)

**Obrázek 20**: zobrazení pro potvrzení odstranění ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image40.png))

Musíme upravit zobrazení indexu tak, aby obsahovalo odkaz pro odstranění záznamů kontaktů (viz obrázek 21). Do stejné buňky tabulky, která obsahuje odkaz pro úpravy, je nutné přidat následující kód:

{. ID = položka. ID})%&gt;

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)

**Obrázek 21**: Zobrazení indexu s odkazem pro úpravy ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image42.png))

Dále je potřeba vytvořit zobrazení pro potvrzení odstranění. Klikněte pravým tlačítkem myši na metodu DELETE () v třídě domovského kontroleru a vyberte možnost nabídky přidat zobrazení. Zobrazí se dialogové okno Přidat zobrazení (viz obrázek 22).

Na rozdíl od v případě zobrazení seznamu, vytvoření a úpravy zobrazení dialog Přidat zobrazení neobsahuje možnost vytvořit zobrazení pro odstranění. Místo toho vyberte třídu data **ContactManager. Models. Contact** a obsah **prázdného** zobrazení. Výběrem možnosti prázdné zobrazení obsahu budete muset vytvořit dodržovali zobrazení.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)

**Obrázek 22**: Přidání zobrazení pro potvrzení odstranění ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image44.png))

Obsah zobrazení odstranění je obsažen v seznamu 9. Toto zobrazení obsahuje formulář, který potvrzuje, jestli by se měl odstranit konkrétní kontakt (viz obrázek 21).

**Výpis 9 – Views\Home\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>Změna názvu výchozího kontroleru

Může vás bother, že název naší třídy Controller pro práci s kontakty se nazývá třída HomeController. Neměli byste mít kontrolér s názvem ContactController?

Tento problém je dostatečně snadný, aby se opravil. Nejdřív je potřeba Refaktorovat název domovského kontroleru. V editoru Visual Studio Code otevřete třídu HomeController, klikněte pravým tlačítkem myši na název třídy a vyberte možnost nabídky **Přejmenovat**. Výběrem této možnosti nabídky se otevře dialogové okno Přejmenovat.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)

**Obrázek 23**: Refaktoring pro název kontroleru ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image46.png))

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)

**Obrázek 24**: použití dialogového okna přejmenovat ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image48.png))

Pokud přejmenujete třídu Controller, Visual Studio aktualizuje také název složky ve složce views. Visual Studio přejmenuje složku \Views\Home na složku \Views\Contact.

Po provedení této změny již aplikace nebude mít k dispozici domovský kontroler. Při spuštění aplikace obdržíte chybovou stránku na obrázku 25.

[![dialogového okna Nový projekt](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)

**Obrázek 25**: žádný výchozí kontroler ([kliknutím zobrazíte obrázek v plné velikosti](iteration-1-create-the-application-vb/_static/image50.png))

Musíme aktualizovat výchozí trasu v souboru Global. asax na použití kontroleru kontaktů místo domovského kontroleru. Otevřete soubor Global. asax a upravte výchozí kontroler používaný výchozí trasou (viz výpis 10).

**Výpis 10-Global. asax. vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

Po provedení těchto změn bude správce kontaktů správně fungovat. Nyní použije třídu Controller kontaktů jako výchozí kontroler.

## <a name="summary"></a>Souhrn

V této první iteraci jsme vytvořili základní aplikaci Správce kontaktů co nejrychleji. Využili jsme výhod sady Visual Studio k vygenerování počátečního kódu pro naše řadiče a zobrazení automaticky. Také jsme využili výhod Entity Framework a automaticky vygenerovat třídy databázového modelu.

V současné době můžete v aplikaci Správce kontaktů vypsat, vytvořit, upravit a odstranit záznamy kontaktů. Jinými slovy můžeme provádět všechny základní databázové operace vyžadované webovou aplikací založenou na databázi.

Omlouváme se, ale naše aplikace obsahuje nějaké problémy. Nejprve a I váhají k tomuto uplatnění aplikace Správce kontaktů není nejoblíbenější aplikace. Potřebuje nějaký návrh práce. V další iteraci se podíváme na to, jak můžeme změnit výchozí stránku předlohy zobrazení a kaskádovou šablonu stylů, aby bylo možné zlepšit vzhled aplikace.

Za druhé jsme neimplementovali žádné ověření formuláře. Například není k dispozici žádné, abyste zabránili odeslání formuláře vytvořit kontakt bez zadání hodnot pro jakékoli pole formuláře. Kromě toho můžete zadat neplatná telefonní čísla a e-mailové adresy. Začneme řešit problém při ověřování formuláře v iteraci #3.

A konečně a nejdůležitější, aktuální iterace aplikace Správce kontaktů se nedá snadno upravovat ani spravovat. Například logika přístupu k databázi je vloženými přímo do akcí kontroleru. To znamená, že nemůžeme upravovat kód pro přístup k datům, aniž byste museli měnit naše řadiče. V pozdějších iteracích prozkoumáme vzory návrhu softwaru, které můžeme implementovat, aby bylo možné změnu správce kontaktů pružně změnit.

> [!div class="step-by-step"]
> [Předchozí](iteration-7-add-ajax-functionality-cs.md)
> [Další](iteration-2-make-the-application-look-nice-vb.md)

---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
title: 'Iterace #2 – nastaví vzhled aplikace jako příjemnéC#() | Microsoft Docs'
author: microsoft
description: V této iteraci Vylepšete vzhled aplikace úpravou výchozí stránky předlohy zobrazení ASP.NET MVC a šablony kaskádových stylů.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1173feb-11ee-4017-8f3f-86599ea6ae13
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-cs
msc.type: authoredcontent
ms.openlocfilehash: 246cb4b4668339cc4b7e4e03ea005102c6a2a5c3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602016"
---
# <a name="iteration-2--make-the-application-look-nice-c"></a>Iterace #2 – nastaví vzhled aplikace jako příjemnéC#()

od [Microsoftu](https://github.com/microsoft)

[Stáhnout kód](iteration-2-make-the-application-look-nice-cs/_static/contactmanager_2_cs1.zip)

> V této iteraci Vylepšete vzhled aplikace úpravou výchozí stránky předlohy zobrazení ASP.NET MVC a šablony kaskádových stylů.

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

Cílem této iterace je zlepšit vzhled aplikace Správce kontaktů. V současné době správce kontaktů používá výchozí stránku předlohy zobrazení ASP.NET MVC a šablonu kaskádových stylů (viz obrázek 1). Tyto věci nevypadají špatně, ale nechci, aby správce kontaktů vypadal stejně jako každý jiný web ASP.NET MVC. Chci tyto soubory nahradit vlastními soubory.

[![dialogového okna Nový projekt](iteration-2-make-the-application-look-nice-cs/_static/image1.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image1.png)

**Obrázek 01**: výchozí vzhled aplikace ASP.NET MVC ([kliknutím zobrazíte obrázek v plné velikosti](iteration-2-make-the-application-look-nice-cs/_static/image2.png))

V této iteraci probereme dva přístupy ke zlepšení vizuálního návrhu naší aplikace. Napřed si ukážeme, jak využít galerii návrhů ASP.NET MVC ke stažení bezplatné šablony návrhu ASP.NET MVC. Galerie návrhů ASP.NET MVC umožňuje vytvořit profesionální webovou aplikaci, aniž by prováděla práci.

Rozhodli jste se Nepoužívat šablonu z Galerie návrhů ASP.NET MVC pro aplikaci Správce kontaktů. Místo toho mám vlastní návrh vytvořený firmou Professional design. V druhé části tohoto kurzu vyberu, jak mám pracovat s profesionální návrhovou společností, která vytvoří konečný návrh ASP.NET MVC.

## <a name="the-aspnet-mvc-design-gallery"></a>Galerie návrhů ASP.NET MVC

Galerie návrhů ASP.NET MVC je bezplatný prostředek poskytovaný společností Microsoft. Galerie ASP.NET MVC se nachází na následující adrese:

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

Galerie návrhů ASP.NET MVC hostuje kolekci bezplatných návrhů webů, které byly vytvořeny speciálně pro použití v projektu ASP.NET MVC. Návrhy jsou odesílány členy komunity. Návštěvníci z Galerie můžou hlasovat o svých oblíbených návrzích (viz obrázek 2).

[![dialogového okna Nový projekt](iteration-2-make-the-application-look-nice-cs/_static/image2.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image3.png)

**Obrázek 02**: galerie návrhů ASP.NET MVC ([kliknutím zobrazíte obrázek v plné velikosti](iteration-2-make-the-application-look-nice-cs/_static/image4.png))

Při psaní tohoto kurzu je nejoblíbenějším návrhem v galerii návrh s názvem říjen od David Hauser. Tento návrh projektu ASP.NET MVC můžete použít provedením následujících kroků:

1. Kliknutím na tlačítko **Stáhnout** Stáhněte soubor říjnu. zip do počítače.
2. Klikněte pravým tlačítkem na stažený soubor. zip a klikněte na tlačítko **odblokování** (viz obrázek 3).
3. Rozbalte soubor do složky s názvem říjen.
4. Vyberte všechny soubory ze složky DesignTemplate obsažené ve složce říjen, klikněte pravým tlačítkem na soubory a vyberte možnost nabídka **Kopírovat**.
5. V okně Visual Studio Průzkumník řešení klikněte pravým tlačítkem na uzel projektu ContactManager a vyberte možnost nabídky **Vložit** (viz obrázek 4).
6. Vyberte možnost nabídky Visual Studio **Upravit, najít a nahradit, rychlé nahrazení** a nahrazení *[MyProjectName]* pomocí *ContactManager* (viz obrázek 5).

[![dialogového okna Nový projekt](iteration-2-make-the-application-look-nice-cs/_static/image3.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image5.png)

**Obrázek 03**: odblokování souboru staženého z webu ([kliknutím zobrazíte obrázek v plné velikosti](iteration-2-make-the-application-look-nice-cs/_static/image6.png))

[![dialogového okna Nový projekt](iteration-2-make-the-application-look-nice-cs/_static/image4.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image7.png)

**Obrázek 04**: přepisování souborů v Průzkumník řešení ([kliknutím zobrazíte obrázek v plné velikosti](iteration-2-make-the-application-look-nice-cs/_static/image8.png))

[![dialogového okna Nový projekt](iteration-2-make-the-application-look-nice-cs/_static/image5.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image9.png)

**Obrázek 05**: nahrazení [projectname] pomocí ContactManager ([kliknutím zobrazíte obrázek v plné velikosti](iteration-2-make-the-application-look-nice-cs/_static/image10.png))

Po dokončení tohoto postupu bude webová aplikace používat nový návrh. Stránka na obrázku 6 znázorňuje vzhled aplikace Contact Manager s návrhem října.

[![dialogového okna Nový projekt](iteration-2-make-the-application-look-nice-cs/_static/image6.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image11.png)

**Obrázek 06**: ContactManager se šablonou říjen ([kliknutím zobrazíte obrázek v plné velikosti](iteration-2-make-the-application-look-nice-cs/_static/image12.png))

## <a name="creating-a-custom-aspnet-mvc-design"></a>Vytvoření vlastního návrhu MVC pro ASP.NET

Galerie návrhů ASP.NET MVC nabízí dobrý výběr různých stylů návrhu. Galerie poskytuje bezproblémově způsob, jak přizpůsobit vzhled aplikací ASP.NET MVC. A samozřejmě má Galerie velkou výhodu, že je zcela zdarma.

Je ale možné, že budete muset vytvořit naprosto jedinečný návrh webu. V takovém případě má smysl pracovat s návrhovou společností na webu. Rozhodli jste se tento postup využít pro návrh aplikace Správce kontaktů.

Jsem správce kontaktů před iterací #1 a projekt odeslal do společnosti pro návrh. Nevlastní sady Visual Studio (Shame na nich!), ale neobsahovaly problém. Mohli byste si zdarma stáhnout Microsoft Visual Web Developer na webu [https://www.asp.net](https://www.asp.net) a otevřít aplikaci Contact Manager v aplikaci Visual Web Developer. Během několika dnů vytvořil návrh na obrázku 7.

[![dialogového okna Nový projekt](iteration-2-make-the-application-look-nice-cs/_static/image7.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image13.png)

**Obrázek 07**: návrh správce kontaktů ASP.NET MVC ([kliknutím zobrazíte obrázek v plné velikosti](iteration-2-make-the-application-look-nice-cs/_static/image14.png))

Nový návrh se skládá ze dvou hlavních souborů: nový soubor šablony stylů a nový soubor hlavní stránky zobrazení. Stránka zobrazení předlohy obsahuje rozložení a sdílený obsah pro zobrazení v aplikaci ASP.NET MVC. Například stránka zobrazení předlohy obsahuje záhlaví, navigační karty a zápatí, které se zobrazí na obrázku 7. Přepsal (a) existující stránku předlohy zobrazení Web. Master ve složce Views\Shared novým souborem Web. Master z návrhové společnosti,

Společnost návrhu také vytvořila novou kaskádovou šablonu stylů a sadu obrázků. Umístil (a) jsem tyto nové soubory do složky obsahu a přepsali jste existující soubor Web. CSS. Veškerý statický obsah byste měli umístit do složky obsahu.

Všimněte si, že nový návrh správce kontaktů obsahuje obrázky pro úpravy a odstraňování kontaktů. Obrázek upravit a odstranit se zobrazí vedle každého kontaktu v tabulce HTML kontaktů.

Původně byly tyto odkazy vykresleny pomocí kódu HTML. Pomocník pro ActionLink () podobný tomuto:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample1.aspx)]

Metoda HTML. ActionLink () nepodporuje obrázky (metoda HTML kóduje text odkazu z bezpečnostních důvodů). Proto jsem nahradil volání HTML. ActionLink () voláními na adresu URL. Action () takto:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-cs/samples/sample2.aspx)]

Metoda HTML. ActionLink () vykresluje celý hypertextový odkaz HTML. Metoda URL. Action () na druhé straně vykresluje pouze adresu URL bez &lt;značku&gt;.

Všimněte si také, že nový návrh zahrnuje vybrané i nevybrané karty. Například na obrázku 8 je vybrána karta **vytvořit nový kontakt** a karta **moje kontakty** není vybrána.

[![dialogového okna Nový projekt](iteration-2-make-the-application-look-nice-cs/_static/image8.jpg)](iteration-2-make-the-application-look-nice-cs/_static/image15.png)

**Obrázek 08**: vybraná a Nevybraná karta ([kliknutím zobrazíte obrázek v plné velikosti](iteration-2-make-the-application-look-nice-cs/_static/image16.png))

Pro podporu vykreslování vybraných i nevybraných karet jsem vytvořili vlastní nápovědu HTML s názvem MenuItemHelper. Tato pomocná metoda vykreslí buď &lt;li&gt; značku, nebo &lt;li Class = "vybraná"&gt; značka v závislosti na tom, zda aktuální kontroler a akce odpovídá kontroleru a názvu akce předané do pomocné rutiny. Kód pro MenuItemHelper je obsažen v seznamu 1.

**Výpis 1 – Helpers\MenuItemHelper.cs**

[!code-csharp[Main](iteration-2-make-the-application-look-nice-cs/samples/sample3.cs)]

MenuItemHelper používá interně TagBuilder třídu pro &lt;sestavení&gt; značky HTML. Třída TagBuilder je velmi užitečná třída nástrojů, kterou můžete použít vždy, když potřebujete vytvořit novou značku jazyka HTML. Obsahuje metody pro přidávání atributů, přidávání tříd šablon stylů CSS, generování identifikátorů a úpravu značky s vnitřním HTML.

## <a name="summary"></a>Souhrn

V této iteraci jsme vylepšili vizuální návrh naší aplikace ASP.NET MVC. Nejdřív jste se zavedli do Galerie návrhů ASP.NET MVC. Zjistili jste, jak stáhnout bezplatné šablony návrhu z Galerie návrhů ASP.NET MVC, kterou můžete použít ve svých aplikacích ASP.NET MVC.

V dalším kroku jsme probrali, jak můžete vytvořit vlastní návrh úpravou výchozího souboru šablony kaskádových stylů a souboru stránky zobrazení předloh. Abychom mohli podpořit nový návrh, museli jsme v naší aplikaci Správce kontaktů udělat nějaké drobné změny. Přidali jsme například novou nápovědu HTML s názvem MenuItemHelper, která zobrazuje vybrané a nevybrané karty.

V další iteraci vydáme velmi důležitý předmět ověřování. Do naší aplikace přidáváme ověřovací kód, aby uživatel nemohl vytvořit nový kontakt bez nutnosti zadat požadované hodnoty, jako je například jméno a příjmení osoby.

> [!div class="step-by-step"]
> [Předchozí](iteration-1-create-the-application-cs.md)
> [Další](iteration-3-add-form-validation-cs.md)

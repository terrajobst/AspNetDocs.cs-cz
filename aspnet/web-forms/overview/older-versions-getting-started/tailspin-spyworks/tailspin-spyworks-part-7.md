---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: '7\. část: Přidání funkcí | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 7 přidává další funkce, jako je například účet revie...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641993"
---
# <a name="part-7-adding-features"></a>7\. část: Přidání funkcí

[Jana Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET. Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.
> 
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 7 přidává další funkce, jako je třeba revize účtu, revize produktů a "Oblíbené položky" a také zakoupené uživatelské ovládací prvky.

## <a id="_Toc260221673"></a>Přidávání funkcí

I když mohou uživatelé procházet náš katalog, umístit položky do svého nákupního košíku a dokončit proces registrace, bude k dispozici celá řada pomocných funkcí, které budeme použít pro zlepšení našeho webu.

1. Recenze účtu (jsou umístěné objednávky seznamu a zobrazí podrobnosti.)
2. Přidejte nějaký konkrétní kontextový obsah na Front-Page.
3. Přidejte funkci, která uživatelům umožní zkontrolovat produkty v katalogu.
4. Vytvoření uživatelského ovládacího prvku pro zobrazení oblíbených položek a umístění tohoto ovládacího prvku na přední stránku.
5. Vytvořte uživatelský ovládací prvek "také koupené" a přidejte jej na stránku s podrobnostmi o produktu.
6. Přidejte stránku kontaktu.
7. Přidejte stránku About.
8. Globální chyba

## <a id="_Toc260221674"></a>Revize účtu

Ve složce Account (účet) vytvořte dvě stránky ASPX One s názvem OrderList. aspx a druhou s názvem OrderDetails. aspx.

OrderList. aspx bude využívat ovládací prvky GridView a EntityDataSource, podobně jako v minulosti.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

EntityDataSource vybere záznamy z tabulky Orders filtrované podle uživatelského jména (viz WhereParameter), kterou nastavíme v proměnné relace, když se přihlásí uživatel.

Všimněte si také těchto parametrů v HyperlinkField ovládacího prvku GridView:

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

Tyto údaje určují odkaz na zobrazení podrobností objednávky pro každý produkt, který určuje pole ČísloObjednávky jako parametr QueryString na stránce OrderDetails. aspx.

## <a id="_Toc260221675"></a>OrderDetails. aspx

Použijeme ovládací prvek EntityDataSource pro přístup k objednávkám a FormView k zobrazení dat objednávek a dalšího objektu EntityDataSource s prvkem GridView k zobrazení všech položek řádku objednávky.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

V souboru kódu na pozadí (OrderDetails.aspx.cs) máme dvě trochu bitů údržbu.

Nejdřív je potřeba zajistit, aby OrderDetails vždy získává ČísloObjednávky.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

Také je potřeba vypočítat a zobrazit celkový součet z položek řádků.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>Domovská stránka

Pojďme na stránku Default. aspx přidat nějaký statický obsah.

Nejprve vytvořím složku Content (obsah) a v ní složku images (a přidám obrázek, který se má použít na domovské stránce.)

Do dolního zástupného znaku stránky default. aspx přidejte následující kód.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>Recenze produktů

Nejprve přidáme tlačítko s odkazem na formulář, který můžeme použít k zadání revize produktu.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

Všimněte si, že do řetězce dotazu předáváme ProductID.

Nyní přidáme stránku s názvem ReviewAdd. aspx.

Tato stránka bude používat ASP.NET AJAX Control Toolkit. Pokud jste to ještě neudělali, můžete si ho stáhnout z [DevExpress](http://devexpress.com/act) a k instalaci sady Toolkit pro použití se sadou Visual Studio zde [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)použít pokyny.

V režimu návrhu přetáhněte ovládací prvky a validátory ze sady nástrojů a sestavte formulář jako ten níže.

![](tailspin-spyworks-part-7/_static/image2.jpg)

Označení bude vypadat přibližně takto.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

Teď, když můžeme zadat recenze, umožňuje zobrazit tyto recenze na stránce produktu.

Přidejte tento kód na stránku ProductDetails. aspx.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

Po spuštění naší aplikace a přechodu na produkt se zobrazí informace o produktu, včetně revizí zákazníků.

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>Ovládací prvek oblíbených položek (vytváření uživatelských ovládacích prvků)

Aby bylo možné zvýšit prodej na vašem webu, přidáme několik funkcí do oblíbených nebo souvisejících produktů v sugestivní prodeji.

První z těchto funkcí bude seznam oblíbených produktů v našem katalogu produktů.

Vytvoříme "uživatelský ovládací prvek", na kterém se zobrazí hlavní položky prodeje na domovské stránce naší aplikace. Vzhledem k tomu, že se jedná o ovládací prvek, můžeme ho použít na libovolné stránce pouhým přetažením ovládacího prvku v návrháři aplikace Visual Studio na libovolnou stránku, kterou se vám líbí.

V Průzkumníku řešení sady Visual Studio klikněte pravým tlačítkem myši na název řešení a vytvořte nový adresář s názvem Controls. I když to není nutné, pomůžeme uchovávat náš projekt tak, že se vytvoří všechny naše uživatelské ovládací prvky v adresáři Controls.

Klikněte pravým tlačítkem na složku ovládací prvky a vyberte možnost Nová položka:

![](tailspin-spyworks-part-7/_static/image4.jpg)

Zadejte název pro náš ovládací prvek "PopularItems". Všimněte si, že Přípona souboru pro uživatelské ovládací prvky je. ascx není. aspx.

Naše oblíbené položky uživatelský ovládací prvek bude definován následujícím způsobem.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

Tady používáme metodu, kterou v této aplikaci zatím nepoužíváme. Používáme ovládací prvek Repeater a místo použití ovládacího prvku zdroje dat zavazujeme ovládací prvek Repeater s výsledky LINQ to Entitiesho dotazu.

V kódu na pozadí našeho ovládacího prvku máme následující postup.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

Všimněte si také tohoto důležitého řádku v horní části kódu našeho ovládacího prvku.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

Vzhledem k tomu, že se Nejoblíbenější položky nemění na základě minut na minuty, můžeme přidat direktivu Aching pro zlepšení výkonu naší aplikace. Tato direktiva způsobí, že bude kód ovládacího prvku proveden pouze v případě, že vyprší výstup v mezipaměti. V opačném případě se použije verze výstupu ovládacího prvku v mezipaměti.

Vše, co je potřeba udělat, je vše, co je náš nový ovládací prvek na naší stránce Default. aspx.

Pomocí přetažení umístěte instanci ovládacího prvku do otevřeného sloupce našeho výchozího formuláře.

![](tailspin-spyworks-part-7/_static/image5.jpg)

Když teď spustíme naši aplikaci, zobrazí se na domovské stránce Nejoblíbenější položky.

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>"Také koupený" ovládací prvek (uživatelské ovládací prvky s parametry)

Druhý uživatelský ovládací prvek, který vytvoříme, bude přebírat sugestivní prodej na další úroveň přidáním kontextu kontextu.

Logika pro výpočet horních "také koupených" položek je netriviální.

Náš "zakoupený" ovládací prvek vybírá záznamy OrderDetails (dříve koupené) pro aktuálně vybrané ProductID a přebírá ČísloObjednávky pro každé nalezené jedinečné pořadí.

Pak z těchto objednávek vybereme možnost Al a nasadíme množství zakoupených produktů. Produkty seřadíme podle tohoto množství součtu a zobrazíme prvních pět položek.

S ohledem na složitost této logiky implementujeme tento algoritmus jako uloženou proceduru.

T-SQL pro uloženou proceduru je následující.

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

Všimněte si, že tato uložená procedura (SelectPurchasedWithProducts) existovala v databázi, když jsme ji zahrnuli do naší aplikace, a když jsme vygenerovali model EDM (Entity Data Model) jsme určili, že kromě tabulek a zobrazení, které potřebujeme, model EDM (Entity Data Model) by měla obsahovat tuto uloženou proceduru.

Pro přístup k uložené proceduře z model EDM (Entity Data Model) musíme tuto funkci naimportovat.

Dvakrát klikněte na model EDM (Entity Data Model) v Průzkumníkovi řešení a otevřete ji v návrháři a otevřete prohlížeč modelů, potom klikněte pravým tlačítkem v návrháři a vyberte Přidat import funkce.

![](tailspin-spyworks-part-7/_static/image1.png)

Tím se otevře dialogové okno.

![](tailspin-spyworks-part-7/_static/image2.png)

Vyplňte pole, jak vidíte výše, vyberte "SelectPurchasedWithProducts" a použijte název procedury pro název naší importované funkce.

Klikněte na OK.

Díky tomu můžeme jednoduše programovat proti uložené proceduře, protože můžeme v modelu provést jinou položku.

Proto v naší "ovládacím prvku" Vytvořte nový uživatelský ovládací prvek s názvem AlsoPurchased. ascx.

Značky pro tento ovládací prvek budou vypadat velmi dobře s ovládacím prvkem PopularItems.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

Významný rozdíl je, že výstupy neukládají do mezipaměti, protože položka, která se má vykreslit, se liší podle produktu.

ProductId bude ovládacímu prvku "vlastnost".

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

V obslužné rutině události PreRender ovládacího prvku jsme EED, že máme tři věci.

1. Ujistěte se, že je ProductID nastaveno.
2. Podívejte se, jestli nejsou k dispozici žádné produkty zakoupené s aktuálním.
3. Výstup některých položek určených v #2.

Všimněte si, jak snadné je volat uloženou proceduru prostřednictvím modelu.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

Až se rozhodnete, že se zakoupí také "zakoupíme", můžeme jednoduše navazovat Repeater na výsledky vrácené dotazem.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

Pokud zde nejsou žádné "zakoupené" položky, jednoduše zobrazíme další oblíbené položky z našeho katalogu.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

Chcete-li zobrazit "zakoupené" položky, otevřete stránku ProductDetails. aspx a přetáhněte ovládací prvek AlsoPurchased z Průzkumníku řešení tak, aby se zobrazil v této pozici ve značce.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

Tím se vytvoří odkaz na ovládací prvek v horní části stránky ProductDetails.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

Vzhledem k tomu, že uživatelský ovládací prvek AlsoPurchased vyžaduje číslo ProductId, nastavíme vlastnost ProductID našeho ovládacího prvku pomocí příkazu Eval pro aktuální položku datového modelu stránky.

![](tailspin-spyworks-part-7/_static/image3.png)

Když teď sestavíme a spustíme a provedeme přechod na produkt, uvidíme také položky koupené.

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> [Předchozí](tailspin-spyworks-part-6.md)
> [Další](tailspin-spyworks-part-8.md)

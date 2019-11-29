---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
title: Použití šablon FormView (VB) | Microsoft Docs
author: rick-anderson
description: Na rozdíl od prvku DetailsView není třída FormView složena z polí. Místo toho je třída FormView vykreslena pomocí šablon. V tomto kurzu se podíváme na použití F...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 67b25f4c-2823-42b6-b07d-1d650b3fd711
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
msc.type: authoredcontent
ms.openlocfilehash: cafe47cf5766bb14503852ec6e9f305d1e6d426f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618410"
---
# <a name="using-the-formviews-templates-vb"></a>Použití šablon FormView (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_14_VB.exe) nebo [Stáhnout PDF](using-the-formview-s-templates-vb/_static/datatutorial14vb1.pdf)

> Na rozdíl od prvku DetailsView není třída FormView složena z polí. Místo toho je třída FormView vykreslena pomocí šablon. V tomto kurzu se podíváme na použití ovládacího prvku FormView k prezentaci méně tuhého zobrazení dat.

## <a name="introduction"></a>Úvod

V posledních dvou kurzech jsme viděli, jak přizpůsobit výstupy ovládacích prvků GridView a DetailsView pomocí TemplateFields. TemplateField umožňují, aby obsah konkrétního pole byl vysoce přizpůsobený, ale na konci mají spíše boxy vzhled jako v mřížce. Pro mnoho scénářů, jako je například rozložení mřížky, je ideální, ale v případě více kapalin je potřeba méně tuhého zobrazení. Při zobrazení jednoho záznamu lze takové rozložení kapalin použít pomocí ovládacího prvku FormView.

Na rozdíl od prvku DetailsView není třída FormView složena z polí. Nelze přidat vlastnost BoundField nebo TemplateField do třídy FormView. Místo toho je třída FormView vykreslena pomocí šablon. Zamyslete se na FormView jako ovládací prvek DetailsView, který obsahuje jednu TemplateField. Třída FormView podporuje následující šablony:

- `ItemTemplate` slouží k vykreslení konkrétního záznamu zobrazeného ve třídě FormView
- `HeaderTemplate` slouží k zadání volitelného řádku záhlaví
- `FooterTemplate` slouží k zadání volitelného řádku zápatí
- `EmptyDataTemplate` Pokud `DataSource` FormView neobsahuje žádné záznamy, použije se `EmptyDataTemplate` místo `ItemTemplate` pro vykreslování značek ovládacího prvku.
- `PagerTemplate` lze použít k přizpůsobení stránkovacího rozhraní pro třídy FormView s povoleným stránkováním
- `EditItemTemplate` / `InsertItemTemplate` použít k přizpůsobení rozhraní pro úpravy nebo vložení rozhraní pro třídy FormView, které podporují tyto funkce

V tomto kurzu se podíváme na použití ovládacího prvku FormView, který prezentuje méně tuhý displej produktů. Namísto polí pro název, kategorii, dodavatele atd. `ItemTemplate` FormView tyto hodnoty zobrazí pomocí kombinace elementu záhlaví a `<table>` (viz obrázek 1).

[![se třída FormView rozdělí z rozložení podobného mřížce zobrazeného v ovládacím prvku DetailsView.](using-the-formview-s-templates-vb/_static/image2.png)](using-the-formview-s-templates-vb/_static/image1.png)

**Obrázek 1**: třída FormView se oddělí z rozložení podobného mřížce zobrazeného v ovládacím prvku DetailsView ([kliknutím zobrazíte obrázek v plné velikosti).](using-the-formview-s-templates-vb/_static/image3.png)

## <a name="step-1-binding-the-data-to-the-formview"></a>Krok 1: vytvoření vazby dat na FormView

Otevřete stránku `FormView.aspx` a přetáhněte FormView ze sady nástrojů na Návrhář. Při prvním přidání třídy FormView se zobrazí jako šedivé pole, které nám dává pokyn, že je potřeba `ItemTemplate`.

[![třída FormView nemůže být vykreslena v návrháři, dokud nebude poskytnuta Šablona ItemTemplate.](using-the-formview-s-templates-vb/_static/image5.png)](using-the-formview-s-templates-vb/_static/image4.png)

**Obrázek 2**: třída FormView se nedá vykreslit v návrháři, dokud není poskytnutý `ItemTemplate` ([kliknutím zobrazíte obrázek v plné velikosti).](using-the-formview-s-templates-vb/_static/image6.png)

`ItemTemplate` lze vytvořit ručně (prostřednictvím deklarativní syntaxe) nebo je lze automaticky vytvořit vytvořením vazby třídy FormView k ovládacímu prvku zdroje dat prostřednictvím návrháře. Tento automaticky vytvořený `ItemTemplate` obsahuje kód HTML, který obsahuje název každého pole a ovládací prvek popisek, jehož vlastnost `Text` je svázána s hodnotou pole. Tento přístup také automaticky vytvoří `InsertItemTemplate` a `EditItemTemplate`, obě jsou vyplněny vstupními ovládacími prvky pro každé datové pole, které je vráceno ovládacím prvkem zdroje dat.

Chcete-li vytvořit šablonu automaticky, z inteligentní značky FormView přidejte nový ovládací prvek ObjectDataSource, který vyvolá metodu `GetProducts()` `ProductsBLL` třídy. Tím se vytvoří třída FormView s `ItemTemplate`, `InsertItemTemplate`a `EditItemTemplate`. Ze zobrazení zdroj odeberte `InsertItemTemplate` a `EditItemTemplate`, protože neuvažujete o vytváření třídy FormView, která podporuje úpravy nebo vložení. Dále vymažte označení v rámci `ItemTemplate`, aby bylo k dispozici čistá břidlicová práce.

Pokud místo toho chcete sestavit `ItemTemplate` ručně, můžete přidat a nakonfigurovat prvek ObjectDataSource přetažením z panelu nástrojů do návrháře. Nenastavte však zdroj dat třídy FormView z návrháře. Místo toho otevřete zobrazení zdroje a ručně nastavte vlastnost `DataSourceID` třídy FormView na hodnotu `ID` prvku ObjectDataSource. Potom ručně přidejte `ItemTemplate`.

Bez ohledu na to, jaký přístup jste se rozhodli přijmout, by deklarativní označení vaší třídy FormView mělo vypadat takto:

[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample1.aspx)]

Chvíli počkejte, než zaškrtnete políčko Povolit stránkování v inteligentní značce FormView; Tím dojde k přidání atributu `AllowPaging="True"` do deklarativní syntaxe třídy FormView. Také nastavte vlastnost `EnableViewState` na hodnotu false.

## <a name="step-2-defining-theitemtemplates-markup"></a>Krok 2: definování značek`ItemTemplate`

S vazbou FormView k ovládacímu prvku ObjectDataSource a nakonfigurovaným pro podporu stránkování je připraveno zadat obsah pro `ItemTemplate`. V tomto kurzu je název produktu zobrazený v nadpisu `<h3>`. V tomto případě použijeme `<table>` HTML pro zobrazení zbývajících vlastností produktu v tabulce se čtyřmi sloupci, kde první a třetí sloupec uvádí názvy vlastností a druhý a čtvrtý seznam jejich hodnot.

Tento kód lze zadat prostřednictvím rozhraní pro úpravu šablony třídy FormView v Návrháři nebo zadat ručně prostřednictvím deklarativní syntaxe. Když pracujete se šablonami, obvykle je rychlejší pracovat přímo s deklarativní syntaxí, ale můžete použít jakoukoli techniku, se kterou jste nejpohodlnější.

Následující kód ukazuje deklarativní značku FormView po dokončení struktury `ItemTemplate`:

[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample2.aspx)]

Všimněte si, že syntaxe datové vazby, například `<%# Eval("ProductName") %>`, může být vložena přímo do výstupu šablony. To znamená, že nemusí být přiřazená k vlastnosti `Text` ovládacího prvku popisek. Například máme `ProductName` hodnota zobrazená v elementu `<h3>` pomocí `<h3><%# Eval("ProductName") %></h3>`, která pro produkt Chai bude vykreslena jako `<h3>Chai</h3>`.

Třídy `ProductPropertyLabel` a `ProductPropertyValue` CSS se používají k určení stylu názvů a hodnot vlastností produktu v `<table>`. Tyto třídy CSS jsou definovány v `Styles.css` a způsobí, že názvy vlastností budou tučné a zarovnané vpravo a přidají se do hodnot vlastností pravé odsazení.

Vzhledem k tomu, že ve třídě FormView nejsou k dispozici žádné CheckBoxFields, aby se zobrazila hodnota `Discontinued` jako zaškrtávací políčko, je nutné přidat vlastní ovládací prvek CheckBox. Vlastnost `Enabled` je nastavena na hodnotu false, je určena pouze pro čtení a vlastnost `Checked` zaškrtávacího políčka je svázána s hodnotou datového pole `Discontinued`.

Po dokončení `ItemTemplate` se informace o produktu zobrazí v mnohem více kapalinovém způsobu. Porovnejte výstup ovládacího prvku DetailsView z posledního kurzu (obrázek 3) s výstupem vygenerovaným ve třídě FormView v tomto kurzu (obrázek 4).

[![tuhý výstup ovládacího prvku DetailsView](using-the-formview-s-templates-vb/_static/image8.png)](using-the-formview-s-templates-vb/_static/image7.png)

**Obrázek 3**: tuhý výstup ovládacího prvku DetailsView ([kliknutím zobrazíte obrázek v plné velikosti](using-the-formview-s-templates-vb/_static/image9.png))

[![výstupu z tekutiny FormView](using-the-formview-s-templates-vb/_static/image11.png)](using-the-formview-s-templates-vb/_static/image10.png)

**Obrázek 4**: výstup kapalinové třídy ([kliknutím zobrazíte obrázek v plné velikosti](using-the-formview-s-templates-vb/_static/image12.png))

## <a name="summary"></a>Přehled

I když ovládací prvky GridView a DetailsView mohou mít svůj výstup přizpůsobený pomocí vlastností TemplateFields, obě budou jejich data prezentovat ve formátu boxy jako Grid. V případech, kdy je třeba jeden záznam zobrazit pomocí méně tuhého rozložení, je třída FormView ideální volbou. Podobně jako ovládací prvek FormView vykreslí jeden záznam z jeho `DataSource`, ale na rozdíl od ovládacího prvku DetailsView se skládá pouze ze šablon a nepodporuje pole.

Jak jsme viděli v tomto kurzu, třída FormView umožňuje pružnější rozložení při zobrazení jednoho záznamu. V budoucích kurzech prověříme ovládací prvky DataList a Repeater, které poskytují stejnou úroveň flexibility jako FormsView, ale mohou zobrazit více záznamů (například GridView).

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Vedoucí recenzent pro tento kurz byl E.R. Gilmore. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](using-templatefields-in-the-detailsview-control-vb.md)
> [Další](displaying-summary-information-in-the-gridview-s-footer-vb.md)

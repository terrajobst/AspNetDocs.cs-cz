---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: Návody použít ovládací prvek ComboBox? (C#) | Microsoft Docs
author: microsoft
description: ComboBox je ovládací prvek ASP.NET AJAX, který kombinuje flexibilitu textového pole se seznamem možností, ze kterých si uživatelé mohou vybrat.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c5fc61300441303b39e348d3eee83b6ee6847b4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554451"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>Návody použít ovládací prvek ComboBox? (C#)

od [Microsoftu](https://github.com/microsoft)

> ComboBox je ovládací prvek ASP.NET AJAX, který kombinuje flexibilitu textového pole se seznamem možností, ze kterých si uživatelé mohou vybrat.

Cílem tohoto kurzu je vysvětlit ovládací prvek ComboBox ovládacího prvku s ovládacím prvkem ovládací prvky AJAX Control Toolkit. Komponenta ComboBox funguje jako kombinace mezi standardním ovládacím prvkem ASP.NET DropDownList a ovládacím prvkem TextBox. Můžete buď vybrat z již existujícího seznamu položek, nebo zadat novou položku.

Pole ComboBox se podobá ovládacímu prvku zařízení automatického dokončování, ale ovládací prvky se používají v různých scénářích. Objekt pro automatické dokončování rozšiřuje webovou službu, aby získal vyhovující položky. Ovládací prvek ComboBox na rozdíl od je inicializován se sadou položek. Použití nástroje pro doplnění automatického dokončování dává smysl při práci s velkým množstvím dat (miliony částí auta) a při použití ovládacího prvku ComboBox dává smysl při práci s malou sadou dat (desítky částí auta).

## <a name="selecting-from-a-static-list-of-items"></a>Výběr ze statického seznamu položek

Pojďme začít s jednoduchou ukázkou použití ovládacího prvku ComboBox. Představte si, že chcete zobrazit statický seznam položek v rozevíracím seznamu. Chcete však ponechat otevřené možnosti, že seznam není úplný. Chcete uživateli dovolit, aby do seznamu zadal vlastní hodnotu.

Vytvoříme novou stránku webových formulářů ASP.NET a použijeme na stránce ovládací prvek ComboBox. Přidejte do projektu novou stránku ASP.NET a přepněte se na zobrazení Návrh.

Pokud chcete na stránce použít ovládací prvek ComboBox, je nutné na stránku přidat ovládací prvek ScriptManager. Přetáhněte ovládací prvek ScriptManager z části pod kartu Rozšíření AJAX na plochu návrháře. Ovládací prvek ScriptManager byste měli přidat v horní části stránky. můžete ji přidat hned pod úvodní &lt;formuláře na straně serveru&gt; značku.

V dalším kroku přetáhněte ovládací prvek ComboBox na stránku. Ovládací prvek ComboBox můžete najít v sadě nástrojů s ostatními ovládacími prvky a ovládacími prvky AJAX Control Toolkit (viz obrázek 1).

[![jednoduchý formulář pro vytvoření vizitky](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**Obrázek 01**: výběr ovládacího prvku ComboBox ze sady nástrojů ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-cs/_static/image2.png))

K zobrazení statického seznamu voleb používáme ovládací prvek ComboBox. Uživatel může pro své jídlo vybrat konkrétní úroveň spiciness ze seznamu tří možností: mírná, střední a horká (viz obrázek 2).

[![výběru ze statického seznamu položek](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**Obrázek 02**: výběr ze statického seznamu položek ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-cs/_static/image4.png))

Existují dva způsoby, jak lze přidat tyto možnosti do ovládacího prvku ComboBox. Nejprve vyberte možnost úlohy upravit možnosti, když najedete myší na ovládací prvek v zobrazení Návrh a otevřete Editor položek (viz obrázek 3).

[![úpravy položek ComboBox](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**Obrázek 03**: úpravy položek ComboBox ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-cs/_static/image6.png))

Druhou možností je přidat seznam položek mezi otevírací a uzavírací &lt;ASP: ComboBox&gt; značky ve zdrojovém zobrazení. Stránka v seznamu 1 obsahuje aktualizovanou položku ComboBox, která obsahuje seznam položek.

**Výpis 1 – statické. aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

Když otevřete stránku v seznamu 1, můžete vybrat jednu z již existujících možností z komponenty ComboBox. Jinými slovy, Komponenta ComboBox funguje stejně jako ovládací prvek DropDownList.

Nicméně máte také možnost zadat novou volbu (například Super Spicy), která není v seznamu existujících. Proto pole ComboBox funguje také jako ovládací prvek TextBox.

Bez ohledu na to, zda jste vybrali již existující položku nebo když zadáte vlastní položku, se vaše volba zobrazí v ovládacím prvku popisek. Při odeslání formuláře se spustí obslužná rutina btnSubmit\_klikněte na ni a aktualizace popisku (viz obrázek 4).

[![zobrazení vybrané položky](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**Obrázek 04**: zobrazení vybrané položky ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-cs/_static/image8.png))

Komponenta ComboBox podporuje stejné vlastnosti jako ovládací prvek DropDownList pro načtení vybrané položky po odeslání formuláře:

- SelectedItem. text – zobrazí hodnotu vlastnosti text vybrané položky.
- SelectedItem. Value – zobrazí hodnotu vlastnosti Value vybrané položky nebo zobrazí text zadaný do pole se seznamem.
- SelectedValue – totéž jako SelectedItem. Value s tím rozdílem, že tato vlastnost umožňuje zadat výchozí (počáteční) vybranou položku.

Pokud do pole ComboBox zadáte vlastní volbu, přiřadí se vlastní volba do vlastností SelectedItem. text i SelectedItem. Value.

## <a name="selecting-the-list-of-items-from-the-database"></a>Výběr seznamu položek z databáze

Můžete načíst seznam položek, které se zobrazí v poli se seznamem z databáze. Můžete například navazovat pole ComboBox na ovládací prvek SqlDataSource, ovládací prvek ObjectDataSource, zdroj LinqDataSource nebo EntityDataSource.

Představte si, že chcete zobrazit seznam filmů v poli se seznamem. Chcete načíst seznam filmů z tabulky databáze filmů. Postupujte následovně:

1. Vytvoření stránky s názvem filmy. aspx
2. Přidejte ovládací prvek ScriptManager na stránku přetažením ovládacího prvku ScriptManager z karty rozšíření AJAX v panelu nástrojů na stránku.
3. Přidejte ovládací prvek ComboBox na stránku přetažením pole se seznamem na stránku.
4. V zobrazení Návrh najeďte myší na ovládací prvek ComboBox a vyberte možnost úloha **Zvolit zdroj dat** (viz obrázek 5). Spustí se Průvodce konfigurací zdroje dat.
5. V kroku **Zvolte zdroj dat** vyberte možnost &lt;nový zdroj dat&gt;.
6. V kroku **Zvolte typ zdroje dat** vyberte databáze.
7. V kroku **Zvolte datové připojení** vyberte svou databázi (například MoviesDB. mdf).
8. V kroku **Uložit připojovací řetězec do konfiguračního souboru aplikace** vyberte možnost uložení připojovacího řetězce.
9. V kroku **Konfigurace příkazu SELECT** vyberte tabulku databáze filmů a vyberte všechny sloupce.
10. V kroku **test Query** klikněte na tlačítko Dokončit.
11. Zpátky v kroku **Zvolit zdroj dat** vyberte sloupec nadpis pro pole, které chcete zobrazit, a sloupec ID pro datové pole (viz obrázek).
12. Kliknutím na tlačítko OK zavřete průvodce.

[![výběru zdroje dat](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**Obrázek 05**: výběr zdroje dat ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-cs/_static/image10.png))

[![výběru polí s datovým textem a hodnotou](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**Obrázek 06**: Výběr polí datového textu a hodnoty ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-cs/_static/image12.png))

Po dokončení kroků uvedených výše je komponenta ComboBox svázána s ovládacím prvkem SqlDataSource, který představuje filmy z tabulky databáze filmů. Zdroj stránky vypadá jako v seznamu 2 (vyčistili jsme formátování trochu).

**Výpis 2 – filmy. aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

Všimněte si, že ovládací prvek ComboBox má vlastnost DataSourceID, která odkazuje na ovládací prvek SqlDataSource. Když otevřete stránku v prohlížeči, zobrazí se seznam filmů z databáze (viz obrázek 7). Můžete buď vybrat video ze seznamu, nebo zadat nový film zadáním videa do pole se seznamem.

[![zobrazení seznamu filmů](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**Obrázek 07**: zobrazení seznamu filmů ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-cs/_static/image14.png))

## <a name="setting-the-dropdownstyle"></a>Nastavení DropDownStyle

Můžete použít vlastnost ComboBox DropDownStyle ke změně chování pole se seznamem. Tato vlastnost přijímá možné hodnoty:

- Rozevírací seznam (výchozí hodnota): ComboBox zobrazuje rozevírací seznam po kliknutí na šipku a můžete zadat vlastní hodnotu.
- Jednoduché – komponenta ComboBox automaticky zobrazuje rozevírací seznam a můžete zadat vlastní hodnotu.
- DropDownList – komponenta ComboBox funguje stejně jako ovládací prvek DropDownList.

Rozdíl mezi rozevíracím seznamem a jednoduchou je při zobrazení seznamu položek. V případě jednoduchého je seznam zobrazen ihned při přesunutí fokusu na pole se seznamem. V případě rozevíracího seznamu je nutné kliknutím na šipku Zobrazit seznam položek.

Hodnota DropDownList způsobí, že ovládací prvek ComboBox funguje stejně jako standardní ovládací prvek DropDownList. Tady je ale důležitý rozdíl. Starší verze aplikace Internet Explorer zobrazí ovládací prvek DropDownList s nekonečným indexem z, takže se ovládací prvek zobrazí před jakýmkoli ovládacím prvkem umístěným před ním. Vzhledem k tomu, že komponenta ComboBox vykresluje značku HTML &lt;div&gt; namísto HTML &lt;vyberte&gt; tag, Komponenta ComboBox správně respektuje řazení z.

## <a name="setting-the-autocompletemode"></a>Nastavení AutoCompleteMode

Vlastnost ComboBox AutoCompleteMode slouží k určení toho, co se stane, když někdo zadá text do pole se seznamem. Tato vlastnost přijímá následující možné hodnoty:

- Žádná – (výchozí hodnota) komponenta ComboBox neposkytuje žádné chování při automatickém dokončení.
- Navrhnout – v poli se zobrazí seznam a zvýrazní se položka, která se shoduje s položkou v seznamu (viz obrázek 8).
- Připojit – komponenta ComboBox nezobrazuje seznam a připojuje shodnou položku ze seznamu do toho, co jste zadali (viz obrázek 9).
- SuggestAppend – Tato komponenta zobrazí seznam a připojí shodnou položku ze seznamu do toho, co jste zadali (viz obrázek 10).

[![se v komponentě ComboBox vytvoří návrh.](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**Obrázek 08**: komponenta ComboBox provede návrh ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-cs/_static/image16.png)).

[![ComboBox připojuje shodný text](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**Obrázek 09**: v poli se seznamem se připojí shodný text ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-cs/_static/image18.png)).

[![navrhuje a přidává pole se seznamem](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**Obrázek 10**: navrhne a připojí se ComboBox ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-combobox-control-cs/_static/image20.png)).

## <a name="summary"></a>Souhrn

V tomto kurzu jste zjistili, jak používat ovládací prvek ComboBox k zobrazení pevné sady položek. Navážeme ovládací prvek ComboBox jak na statickou sadu položek, tak na databázovou tabulku. Nakonec jste zjistili, jak upravit chování komponenty ComboBox nastavením vlastností DropDownStyle a AutoCompleteMode.

> [!div class="step-by-step"]
> [Next](how-do-i-use-the-combobox-control-vb.md)

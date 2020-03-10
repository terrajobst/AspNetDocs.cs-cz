---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-vb
title: Použití vlastností TemplateField v ovládacím prvku GridView (VB) | Microsoft Docs
author: rick-anderson
description: Chcete-li poskytnout flexibilitu, prvek GridView nabídne pole TemplateField, které se vykreslí pomocí šablony. Šablona může zahrnovat kombinaci statických ovládacích prvků HTML, webové ovládací prvky a...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: a92cd6ed-609a-4e40-ad23-004b54afd436
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 3c090dbf65d9acbcc0e343cda5e8da7fff2d35d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78531477"
---
# <a name="using-templatefields-in-the-gridview-control-vb"></a>Použití vlastností TemplateField v ovládacím prvku GridView (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_12_VB.exe) nebo [Stáhnout PDF](using-templatefields-in-the-gridview-control-vb/_static/datatutorial12vb1.pdf)

> Chcete-li poskytnout flexibilitu, prvek GridView nabídne pole TemplateField, které se vykreslí pomocí šablony. Šablona může zahrnovat kombinaci statických prvků HTML, webové ovládací prvky a syntaxe datových vazeb. V tomto kurzu podíváme se, jak použít TemplateField k dosažení větší úrovně přizpůsobení pomocí ovládacího prvku GridView.

## <a name="introduction"></a>Úvod

Prvek GridView se skládá ze sady polí, které určují, jaké vlastnosti z `DataSource` mají být zahrnuty do vykresleného výstupu spolu s tím, jak se data budou zobrazovat. Nejjednodušší typ pole je vlastnost BoundField, který zobrazuje datovou hodnotu jako text. Jiné typy polí zobrazují data pomocí alternativních prvků HTML. Třídě CheckBoxField podporována se například vykresluje jako zaškrtávací políčko, jehož zaškrtnutý stav závisí na hodnotě zadaného datového pole; ImageField vykreslí obrázek, jehož zdroj obrázku je založen na zadaném datovém poli. Hypertextové odkazy a tlačítka, jejichž stav závisí na hodnotě podkladového datového pole, lze vykreslit pomocí typů polí HyperLinkField a ButtonField.

I když typy polí třídě CheckBoxField podporována, ImageField, HyperLinkField a ButtonField umožňují alternativní zobrazení dat, jsou stále poměrně omezené s ohledem na formátování. Třídě CheckBoxField podporována může zobrazit pouze jedno zaškrtávací políčko, zatímco ImageField může zobrazit pouze jeden obrázek. Co když konkrétní pole potřebuje zobrazit nějaký text, zaškrtávací políčko a obrázek, *a* to vše založené na různých hodnotách datových polí? Nebo co když chtěli zobrazit data pomocí jiného webového ovládacího prvku, než je zaškrtávací políčko, obrázek, hypertextový odkaz nebo tlačítko? Vlastnost BoundField navíc omezuje zobrazení na jedno datové pole. Co když jsme chtěli v jednom sloupci GridViewu zobrazit dvě nebo víc hodnot datových polí?

Chcete-li přizpůsobit tuto úroveň flexibility, ovládací prvek GridView nabídne pole TemplateField, které se vykreslí pomocí *šablony*. Šablona může zahrnovat kombinaci statických prvků HTML, webové ovládací prvky a syntaxe datových vazeb. TemplateField má navíc celou řadu šablon, které lze použít k přizpůsobení vykreslování pro různé situace. Například `ItemTemplate` se ve výchozím nastavení používá k vykreslení buňky pro každý řádek, ale šablonu `EditItemTemplate` lze použít k přizpůsobení rozhraní při úpravě dat.

V tomto kurzu podíváme se, jak použít TemplateField k dosažení větší úrovně přizpůsobení pomocí ovládacího prvku GridView. V [předchozím kurzu](custom-formatting-based-upon-data-vb.md) jsme viděli, jak přizpůsobit formátování na základě podkladových dat pomocí obslužných rutin událostí `DataBound` a `RowDataBound`. Další způsob přizpůsobení formátování na základě podkladových dat je voláním metod formátování v rámci šablony. V tomto kurzu se podíváme i na tuto techniku.

Pro účely tohoto kurzu použijeme pole TemplateFields k přizpůsobení vzhledu seznamu zaměstnanců. Konkrétně vypíšeme všechny zaměstnance, ale zobrazí se první a poslední jméno zaměstnance v jednom sloupci, datum přijetí v ovládacím prvku Kalendář a sloupec stav, který označuje, kolik dní se ve společnosti zaměstnano.

[pro přizpůsobení zobrazení se používají tři pole TemplateField ![.](using-templatefields-in-the-gridview-control-vb/_static/image2.png)](using-templatefields-in-the-gridview-control-vb/_static/image1.png)

**Obrázek 1**: k přizpůsobení zobrazení se používají tři pole TemplateField ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-gridview-control-vb/_static/image3.png)).

## <a name="step-1-binding-the-data-to-the-gridview"></a>Krok 1: vytvoření vazby dat k prvku GridView

Ve scénářích vytváření sestav, kdy potřebujete použít TemplateFields k přizpůsobení vzhledu, je nejjednodušší začít vytvořením ovládacího prvku GridView, který obsahuje pouze BoundFields, a pak přidáním nových TemplateFields nebo převodem existující BoundFields na TemplateField podle potřeby. Proto tento kurz spusťte přidáním prvku GridView na stránku pomocí návrháře a navážeme jej na prvek ObjectDataSource, který vrátí seznam zaměstnanců. Pomocí těchto kroků se vytvoří prvek GridView s BoundFields pro každé pole zaměstnance.

Otevřete stránku `GridViewTemplateField.aspx` a přetáhněte prvek GridView z panelu nástrojů do návrháře. Z inteligentní značky prvku GridView vyberte, chcete-li přidat nový ovládací prvek ObjectDataSource, který vyvolá metodu `GetEmployees()` `EmployeesBLL` třídy.

[![přidat nový ovládací prvek ObjectDataSource, který vyvolá metodu GetEmployees ()](using-templatefields-in-the-gridview-control-vb/_static/image5.png)](using-templatefields-in-the-gridview-control-vb/_static/image4.png)

**Obrázek 2**: Přidání nového ovládacího prvku ObjectDataSource, který vyvolá metodu `GetEmployees()` ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-gridview-control-vb/_static/image6.png))

Vazba prvku GridView tímto způsobem automaticky přidá vlastnost BoundField pro každou z vlastností zaměstnanců: `EmployeeID`, `LastName`, `FirstName`, `Title`, `HireDate`, `ReportsTo`a `Country`. Pro tuto sestavu není bother se zobrazením vlastností `EmployeeID`, `ReportsTo`nebo `Country`. Pokud chcete tyto BoundFields odebrat, můžete:

- Pomocí dialogového okna pole klikněte na odkaz Upravit sloupce z inteligentní značky GridViewu a zobrazte toto dialogové okno. Potom v levém dolním seznamu vyberte BoundFields a kliknutím na červené X odeberte vlastnost BoundField.
- Upravte deklarativní syntaxi ovládacího prvku GridView ze zobrazení zdroje a odstraňte prvek `<asp:BoundField>` pro vlastnost BoundField, který chcete odebrat.

Po odebrání `EmployeeID`, `ReportsTo`a `Country` BoundFields by vaše značky GridViewu měly vypadat takto:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample1.aspx)]

Počkejte, než se vám zobrazí náš průběh v prohlížeči. V tomto okamžiku byste měli vidět tabulku se záznamem pro každého zaměstnance a čtyři sloupce: jednu pro příjmení zaměstnance, jednu pro jejich křestní jméno, jednu pro svůj název a jednu pro datum přijetí.

[![polí LastName, FirstName, title a HireDate se zobrazí pro každého zaměstnance.](using-templatefields-in-the-gridview-control-vb/_static/image8.png)](using-templatefields-in-the-gridview-control-vb/_static/image7.png)

**Obrázek 3**: pole `LastName`, `FirstName`, `Title`a `HireDate` se zobrazují pro každého zaměstnance ([kliknutím zobrazíte obrázek v plné velikosti).](using-templatefields-in-the-gridview-control-vb/_static/image9.png)

## <a name="step-2-displaying-the-first-and-last-names-in-a-single-column"></a>Krok 2: zobrazení křestní jméno a příjmení v jednom sloupci

V současné době se jméno a příjmení každého zaměstnance zobrazí v samostatném sloupci. Je možné, že budou místo toho kombinovány do jednoho sloupce. K tomu musíme použít TemplateField. Můžeme buď přidat nové pole TemplateField, přidat k němu potřebné syntaxe kódu a datové vazby a pak odstranit `FirstName` a `LastName` BoundFields, nebo můžeme převést `FirstName` vlastnost BoundField na TemplateField, upravit pole TemplateField tak, aby zahrnovalo `LastName` hodnotu, a pak odebrat `LastName` vlastnost BoundField.

Oba přístupy mají stejný výsledek, ale vlastní I, jako je převod BoundFields na TemplateField, pokud je to možné, protože převod automaticky přidává `ItemTemplate` a `EditItemTemplate` s webovými ovládacími prvky a syntaxí datových vazeb, aby napodoboval vzhled a funkce vlastnost BoundField. Výhodou je, že budeme muset udělat méně práce s TemplateField, protože proces převodu provede nějakou práci pro nás.

Chcete-li převést existující vlastnost BoundField na TemplateField, klikněte na odkaz Upravit sloupce z inteligentní značky GridView, čímž otevřete dialogové okno pole. V levém dolním rohu vyberte vlastnost BoundField, který chcete převést, a potom v pravém dolním rohu klikněte na odkaz převést toto pole na TemplateField.

[![převést vlastnost BoundField na TemplateField z dialogového okna pole](using-templatefields-in-the-gridview-control-vb/_static/image11.png)](using-templatefields-in-the-gridview-control-vb/_static/image10.png)

**Obrázek 4**: převod vlastnost BoundField na TemplateField z dialogového okna pole ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-gridview-control-vb/_static/image12.png))

Pokračujte a převeďte `FirstName` vlastnost BoundField na TemplateField. Po této změně není v Návrháři žádný Perceptive rozdíl. Důvodem je, že převod vlastnost BoundField na TemplateField vytvoří TemplateField, který udržuje vzhled a chování vlastnost BoundField. Navzdory tomu, že v tomto okamžiku není v Návrháři žádný vizuální rozdíl, tento proces převodu nahradil deklarativní Syntax vlastnost BoundField-`<asp:BoundField DataField="FirstName" HeaderText="FirstName" SortExpression="FirstName" />`-s následující syntaxí TemplateField:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample2.aspx)]

Jak vidíte, pole TemplateField se skládá ze dvou šablon `ItemTemplate`, které mají popisek, jehož vlastnost `Text` je nastavena na hodnotu `FirstName` datové pole, a `EditItemTemplate` s ovládacím prvkem TextBox, jehož vlastnost `Text` je také nastavena na `FirstName` datové pole. Syntaxe datové vazby-`<%# Bind("fieldName") %>` – určuje, že datové pole *`fieldName`* je vázáno na zadanou vlastnost webového ovládacího prvku.

Chcete-li do této třídy TemplateField přidat hodnotu datového pole `LastName`, musíme do `ItemTemplate` přidat další webový ovládací prvek popisek a vytvořit jeho vlastnost `Text` `LastName`. To lze provést buď ručně, nebo prostřednictvím návrháře. Pokud to chcete provést ručně, jednoduše přidejte do `ItemTemplate`příslušnou deklarativní syntaxi:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample3.aspx)]

Chcete-li jej přidat pomocí návrháře, klikněte na odkaz Upravit šablony z inteligentní značky prvku GridView. Tím se zobrazí rozhraní pro úpravu šablony prvku GridView. V rámci inteligentní značky tohoto rozhraní je seznam šablon v prvku GridView. Vzhledem k tomu, že v tuto chvíli máme jenom jednu TemplateField, jediné šablony uvedené v rozevíracím seznamu jsou šablony pro `FirstName` TemplateField společně s `EmptyDataTemplate` a `PagerTemplate`. `EmptyDataTemplate` šablona, je-li zadána, je použita k vykreslení výstupu prvku GridView, pokud nejsou k dispozici žádné výsledky v datech svázaných s ovládacím prvek GridView; `PagerTemplate`, je-li tento parametr zadán, slouží k vykreslení stránkování rozhraní prvku GridView, který podporuje stránkování.

[![šablon prvku GridView lze upravovat pomocí návrháře.](using-templatefields-in-the-gridview-control-vb/_static/image14.png)](using-templatefields-in-the-gridview-control-vb/_static/image13.png)

**Obrázek 5**: šablony prvku GridView lze upravovat pomocí návrháře ([kliknutím zobrazíte obrázek v plné velikosti).](using-templatefields-in-the-gridview-control-vb/_static/image15.png)

Chcete-li také zobrazit `LastName` v `FirstName` TemplateField přetáhněte ovládací prvek popisek ze sady nástrojů do `ItemTemplate` `FirstName` TemplateField v rozhraní pro úpravu šablony prvku GridView.

[![přidat webový ovládací prvek popisku do šablony ItemTemplate TemplateField ' FirstName '](using-templatefields-in-the-gridview-control-vb/_static/image17.png)](using-templatefields-in-the-gridview-control-vb/_static/image16.png)

**Obrázek 6**: Přidejte ovládací prvek web popisku do objektu ItemTemplate `FirstName` TemplateField ([kliknutím zobrazíte obrázek v plné velikosti).](using-templatefields-in-the-gridview-control-vb/_static/image18.png)

V tuto chvíli webový ovládací prvek popisku přidaný do TemplateField má jeho vlastnost `Text` nastavenou na "label". Musíme to změnit, aby byla tato vlastnost vázána na hodnotu datového pole `LastName`. Chcete-li to provést, klikněte na inteligentní značku ovládacího prvku popisek a vyberte možnost Upravit datové vazby.

[![vyberte možnost Upravit datové vazby z inteligentní značky popisku.](using-templatefields-in-the-gridview-control-vb/_static/image20.png)](using-templatefields-in-the-gridview-control-vb/_static/image19.png)

**Obrázek 7**: vyberte možnost Upravit datové vazby z inteligentní značky popisku ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-gridview-control-vb/_static/image21.png)).

Tím se zobrazí dialogové okno datové vazby. Z tohoto místa můžete vybrat vlastnost, která se má zúčastnit vazby ze seznamu na levé straně, a zvolit pole, k němuž chcete navázat data z rozevíracího seznamu na pravé straně. Na levé straně a `LastName` pole vyberte vlastnost `Text` a klikněte na OK.

[![vytvořit vazby vlastnosti text k datovému poli LastName](using-templatefields-in-the-gridview-control-vb/_static/image23.png)](using-templatefields-in-the-gridview-control-vb/_static/image22.png)

**Obrázek 8**: svázání vlastnosti `Text` s datovým polem `LastName` ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-gridview-control-vb/_static/image24.png))

> [!NOTE]
> Dialogové okno datové vazby vám umožní určit, jestli se má provést Obousměrná vazba. Pokud necháte toto políčko nezaškrtnuté, použije se místo `<%# Bind("LastName")%>``<%# Eval("LastName")%>` syntaxe datové vazby. V tomto kurzu je to pro tento kurz přesné. Obousměrná vazba se při vkládání a úpravách dat bude důležitá. V případě, že se ale jednoduše zobrazují data, ale oba postupy budou fungovat stejně dobře. V budoucích kurzech se podrobněji podíváme na oboustrannou datovou vazbu.

Chvíli počkejte, než tuto stránku zobrazíte v prohlížeči. Jak vidíte, prvek GridView stále obsahuje čtyři sloupce; sloupec `FirstName` nyní *ale obsahuje hodnoty* polí `FirstName` a `LastName` dat.

[![hodnoty FirstName i LastName se zobrazují v jednom sloupci.](using-templatefields-in-the-gridview-control-vb/_static/image26.png)](using-templatefields-in-the-gridview-control-vb/_static/image25.png)

**Obrázek 9**: hodnoty `FirstName` i `LastName` se zobrazují v jednom sloupci ([kliknutím zobrazíte obrázek v plné velikosti).](using-templatefields-in-the-gridview-control-vb/_static/image27.png)

Chcete-li dokončit tento první krok, odeberte `LastName` vlastnost BoundField a přejmenujte vlastnost `HeaderText` `FirstName` TemplateField na "Name". Po těchto změnách by deklarativní označení prvku GridView mělo vypadat takto:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample4.aspx)]

[![jméno a příjmení každého zaměstnance se zobrazí v jednom sloupci.](using-templatefields-in-the-gridview-control-vb/_static/image29.png)](using-templatefields-in-the-gridview-control-vb/_static/image28.png)

**Obrázek 10**: jméno a příjmení každého zaměstnance se zobrazí v jednom sloupci ([kliknutím zobrazíte obrázek v plné velikosti).](using-templatefields-in-the-gridview-control-vb/_static/image30.png)

## <a name="step-3-using-the-calendar-control-to-display-thehireddatefield"></a>Krok 3: použití ovládacího prvku kalendář k zobrazení pole`HiredDate`

Zobrazení hodnoty datového pole jako textu v prvku GridView je jednoduché jako použití vlastnost BoundField. V některých scénářích se ale data nejlépe vyjadřují pomocí konkrétního webového ovládacího prvku namísto jenom textu. Toto přizpůsobení zobrazení dat je možné u vlastností TemplateFields. Například namísto zobrazení data přijetí zaměstnance jako textu jsme mohli zobrazit kalendář (pomocí [ovládacího prvku Kalendář](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar(VS.80).aspx)) se zvýrazněným datem přijetí.

Chcete-li to dosáhnout, začněte převodem `HiredDate` vlastnost BoundField na TemplateField. Jednoduše přejděte na inteligentní značku prvku GridView a klikněte na odkaz Upravit sloupce a otevřete dialogové okno pole. Vyberte `HiredDate` vlastnost BoundField a klikněte na převést toto pole na TemplateField.

[![převést vlastnost BoundField HiredDate na TemplateField](using-templatefields-in-the-gridview-control-vb/_static/image32.png)](using-templatefields-in-the-gridview-control-vb/_static/image31.png)

**Obrázek 11**: převeďte `HiredDate` vlastnost BoundField na TemplateField ([kliknutím zobrazíte obrázek v plné velikosti).](using-templatefields-in-the-gridview-control-vb/_static/image33.png)

Jak jsme viděli v kroku 2, nahradí vlastnost BoundField výrazem TemplateField, který obsahuje `ItemTemplate` a `EditItemTemplate` pomocí popisku a textového pole, jehož vlastnosti `Text` jsou vázané na `HiredDate` hodnotu pomocí `<%# Bind("HiredDate")%>`syntaxe datové vazby.

Chcete-li text nahradit ovládacím prvkem kalendáře, upravte šablonu odebráním popisku a přidáním ovládacího prvku kalendáře. Z návrháře vyberte možnost Upravit šablony z inteligentní značky GridView a v rozevíracím seznamu zvolte `ItemTemplate` `HireDate` TemplateField. Dále odstraňte ovládací prvek popisek a přetáhněte ovládací prvek Kalendář ze sady nástrojů do rozhraní pro úpravu šablony.

[![přidání ovládacího prvku kalendáře do šablony ItemTemplate elementu ZaměstnánOd TemplateField](using-templatefields-in-the-gridview-control-vb/_static/image35.png)](using-templatefields-in-the-gridview-control-vb/_static/image34.png)

**Obrázek 12**: Přidání ovládacího prvku kalendáře do `ItemTemplate` `HireDate` TemplateField ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-gridview-control-vb/_static/image36.png))

V tomto okamžiku každý řádek prvku GridView bude obsahovat ovládací prvek kalendáře ve svém `HiredDate` TemplateField. Skutečná `HiredDate`ová hodnota zaměstnance ale není nastavená kdekoli v ovládacím prvku Kalendář, což způsobí, že každý ovládací prvek Kalendář bude ve výchozím nastavení zobrazovat aktuální měsíc a datum. Pokud to chcete napravit, musíme každému zaměstnanci přiřadit `HiredDate` vlastnosti [SelectedDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selecteddate(VS.80).aspx) a [VisibleDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.visibledate(VS.80).aspx) ovládacího prvku kalendáře.

Z inteligentní značky ovládacího prvku Kalendář vyberte možnost Upravit datové vazby. Dále navažte `SelectedDate` i `VisibleDate` vlastností do pole `HiredDate` dat.

[![navazovat vlastnosti SelectedDate a VisibleDate na datové pole HiredDate](using-templatefields-in-the-gridview-control-vb/_static/image38.png)](using-templatefields-in-the-gridview-control-vb/_static/image37.png)

**Obrázek 13**: svázání vlastností `SelectedDate` a `VisibleDate` s datovým polem `HiredDate` ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-gridview-control-vb/_static/image39.png))

> [!NOTE]
> Vybrané datum ovládacího prvku kalendáře nemusí být nutně viditelné. Například kalendář může mít 1<sup>St</sup>. srpna 1999 jako vybrané datum, ale zobrazuje aktuální měsíc a rok. Vybrané datum a viditelné datum jsou určené `SelectedDate` a `VisibleDate` vlastností ovládacího prvku kalendáře. Vzhledem k tomu, že chceme vybrat `HiredDate` zaměstnanců a ujistit se, že je vidět, že je potřeba vytvořit vazby obou těchto vlastností na `HireDate` datové pole.

Po zobrazení stránky v prohlížeči teď kalendář zobrazuje měsíc data přijetí zaměstnance a vybere konkrétní datum.

[v ovládacím prvku Kalendář se zobrazí ![HiredDate zaměstnanců.](using-templatefields-in-the-gridview-control-vb/_static/image41.png)](using-templatefields-in-the-gridview-control-vb/_static/image40.png)

**Obrázek 14**: `HiredDate` zaměstnanců se zobrazí v ovládacím prvku Kalendář ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-gridview-control-vb/_static/image42.png)).

> [!NOTE]
> V rozporu se všemi příklady, které jsme doposud viděli, *ale* pro tento kurz jsme nastavili vlastnost `EnableViewState` na `False` pro tento prvek GridView. Důvodem pro toto rozhodnutí je, že když kliknete na data ovládacího prvku Kalendář, dojde k postbacku, nastavení vybraného kalendářního data na datum, na které jste klikli. Je-li stav zobrazení prvku GridView zakázán, ale při každém postbacku jsou data ovládacího prvku GridView svázána s podkladovým zdrojem dat, což způsobí, že vybrané datum kalendáře bude nastaveno *zpět* na `HireDate`zaměstnanců a přepíše datum zvolené uživatelem.

Pro účely tohoto kurzu se jedná o moot diskuzi, protože uživatel nemůže aktualizovat `HireDate`zaměstnanců. Bylo by pravděpodobně vhodné nakonfigurovat ovládací prvek kalendáře tak, aby jeho data nebyla zvolena. V tomto kurzu se dozvíte, že v některých případech musí být stav zobrazení povolený, aby bylo možné zajistit určitou funkčnost.

## <a name="step-4-showing-the-number-of-days-the-employee-has-worked-for-the-company"></a>Krok 4: zobrazení počtu dnů, po které zaměstnanec pracoval pro společnost

Zatím jsme viděli dvě aplikace TemplateField:

- Kombinování dvou nebo více hodnot datových polí do jednoho sloupce a
- Vyjádření hodnoty datového pole pomocí webového ovládacího prvku místo textu

Třetí použití TemplateFields je v zobrazení metadat týkajících se podkladových dat prvku GridView. Kromě toho, že se zobrazují data přijetí zaměstnanců, například můžeme chtít mít sloupec, který zobrazuje počet dní, po které jsou úlohy v úloze.

Ještě jiné použití TemplateFields nastane ve scénářích, kdy se musí podkladová data zobrazit odlišně v sestavě webové stránky, než ve formátu, který je uložen v databázi. Představte si, že `Employees` tabulka obsahovala `Gender` pole, které uložilo znak `M` nebo `F` k označení pohlaví zaměstnance. Při zobrazování těchto informací na webové stránce můžeme chtít zobrazit pohlaví jako "samci" nebo "žena", a to na rozdíl od "M" nebo "F".

Oba tyto scénáře lze zpracovat vytvořením *metody formátování* ve třídě kódu na pozadí stránky ASP.NET (nebo v samostatné knihovně tříd implementované jako metoda `Shared`), která je vyvolána ze šablony. Tato metoda formátování je vyvolána ze šablony pomocí stejné syntaxe datové vazby, která se zobrazila dříve. Metoda formátování může přebírat libovolný počet parametrů, ale musí vracet řetězec. Tímto vráceným řetězcem je kód HTML, který je vložen do šablony.

Pro ilustraci tohoto konceptu si podíváme náš kurz a zobrazí se sloupec, ve kterém se zobrazí celkový počet dnů, po které se zaměstnanec v úloze nachází. Tato metoda formátování převezme objekt `Northwind.EmployeesRow` a vrátí počet dní, po které zaměstnanec zaměstnán jako řetězec. Tato metoda může být přidána do třídy kódu na pozadí stránky ASP.NET, ale *musí* být označena jako `Protected` nebo `Public`, aby mohla být z šablony přístupná.

[!code-vb[Main](using-templatefields-in-the-gridview-control-vb/samples/sample5.vb)]

Vzhledem k tomu, že pole `HiredDate` může obsahovat `NULL` hodnot databáze, musíte nejdřív zajistit, aby před pokračováním výpočtu nebyla hodnota `NULL`. Pokud je hodnota `HiredDate` `NULL`, jednoduše vrátíme řetězec "unknown"; Pokud není `NULL`, vypočítáme rozdíl mezi aktuálním časem a hodnotou `HiredDate` a vrátíte počet dní.

Aby bylo možné využít tuto metodu, je nutné ji vyvolat z pole TemplateField v prvku GridView pomocí syntaxe datové vazby. Začněte přidáním nového TemplateField do prvku GridView kliknutím na odkaz Upravit sloupce v inteligentní značce prvku GridView a přidáním nového prvku TemplateField.

[![přidat do prvku GridView novou hodnotu TemplateField](using-templatefields-in-the-gridview-control-vb/_static/image44.png)](using-templatefields-in-the-gridview-control-vb/_static/image43.png)

**Obrázek 15**: Přidání nového pole TemplateField do prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-gridview-control-vb/_static/image45.png))

Nastavte tuto novou vlastnost `HeaderText` TemplateField na "dny v úloze" a jeho vlastnost `HorizontalAlign` `ItemStyle`na `Center`. Chcete-li volat metodu `DisplayDaysOnJob` ze šablony, přidejte `ItemTemplate` a použijte následující syntaxi datové vazby:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample6.aspx)]

`Container.DataItem` vrátí objekt `DataRowView` odpovídající záznamu `DataSource` navázanému na `GridViewRow`. Jeho vlastnost `Row` vrací `Northwind.EmployeesRow`silného typu, který je předán metodě `DisplayDaysOnJob`. Tato syntaxe datové vazby se může zobrazit přímo v `ItemTemplate` (jak je znázorněno v deklarativní syntaxi níže) nebo může být přiřazena vlastnosti `Text` webového ovládacího prvku popisku.

> [!NOTE]
> Alternativně namísto předání v `EmployeesRow` instance můžeme jednoduše předat hodnotu `HireDate` pomocí `<%# DisplayDaysOnJob(Eval("HireDate")) %>`. Nicméně metoda `Eval` vrátí `Object`, takže by bylo nutné změnit signaturu `DisplayDaysOnJob` metody, aby se místo toho přijal vstupní parametr typu `Object`. `Eval("HireDate")` volání do `DateTime` nemůžeme obsadit, protože sloupec `HireDate` v tabulce `Employees` může obsahovat `NULL` hodnoty. Proto je potřeba přijmout jako vstupní parametr pro metodu `DisplayDaysOnJob` `Object`, zkontrolujte, zda má `NULL` hodnotu databáze (kterou lze dosáhnout pomocí `Convert.IsDBNull(objectToCheck)`), a pak pokračujte v souladu s odpovídajícím způsobem.

Vzhledem k těmto odlišností jsem se rozhodli předat celou instanci `EmployeesRow`. V dalším kurzu se zobrazí další příklad pro použití syntaxe `Eval("columnName")` pro předání vstupního parametru do metody formátování.

Následující znázorňuje deklarativní syntaxi pro náš prvek GridView po přidání TemplateField a metodu `DisplayDaysOnJob` volanou z `ItemTemplate`:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-vb/samples/sample7.aspx)]

Obrázek 16 znázorňuje dokončený kurz při prohlížení v prohlížeči.

[![počet dní, po který se zaměstnanec v úloze zobrazuje](using-templatefields-in-the-gridview-control-vb/_static/image47.png)](using-templatefields-in-the-gridview-control-vb/_static/image46.png)

**Obrázek 16**: počet dní, po který se zaměstnanec v úloze zobrazuje ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-gridview-control-vb/_static/image48.png))

## <a name="summary"></a>Souhrn

Pole TemplateField v ovládacím prvku GridView umožňuje dosáhnout vyšší úrovně flexibility při zobrazování dat, než je k dispozici pro ostatní ovládací prvky pole. TemplateFields jsou ideální pro situace, kde:

- V jednom sloupci GridView se musí zobrazit víc datových polí.
- Data se nejlépe vyjadřují pomocí webového ovládacího prvku místo prostého textu.
- Výstup závisí na podkladových datech, jako je například zobrazení metadat nebo přeformátování dat.

K přizpůsobení zobrazení dat se také používají pole TemplateField pro přizpůsobení uživatelských rozhraní používaných pro úpravy a vkládání dat, jak uvidíme v budoucích kurzech.

Další dva kurzy pokračují v zkoumání šablon, počínaje tím, že se podíváte na použití vlastností TemplateField v prvku DetailsView. Za tímto účelem zapnete FormView, který používá šablony namísto polí k zajištění větší flexibility v rozložení a struktuře dat.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor potenciálních zákazníků pro tento kurz byl Dan Jagers. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](custom-formatting-based-upon-data-vb.md)
> [Další](using-templatefields-in-the-detailsview-control-vb.md)

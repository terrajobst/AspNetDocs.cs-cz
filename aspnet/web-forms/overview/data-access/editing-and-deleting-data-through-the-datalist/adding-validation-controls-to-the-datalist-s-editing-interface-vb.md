---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-vb
title: Přidání validačních ovládacích prvků do rozhraní pro úpravy prvku DataList (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se dozvíte, jak snadné je přidat ověřovací ovládací prvky do EditItemTemplate prvku DataList, aby se zajistilo více foolproof úprav uživatele int...
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 6b073fc6-524d-453d-be7c-0c30986de391
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: f952a7bb95e956a2ad935f8bdef5c3efa7437ecb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621830"
---
# <a name="adding-validation-controls-to-the-datalists-editing-interface-vb"></a>Přidání validačních ovládacích prvků do rozhraní pro úpravy prvku DataList (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_39_VB.exe) nebo [Stáhnout PDF](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/datatutorial39vb1.pdf)

> V tomto kurzu se dozvíte, jak snadné je přidat ověřovací ovládací prvky do EditItemTemplate prvku DataList, aby bylo možné zajistit další foolproof úpravy uživatelského rozhraní.

## <a name="introduction"></a>Úvod

V prozatímných kurzech upravujících úpravy ovládacího prvku DataList nezahrnovala žádná aktivní ověřování vstupu uživatele, i když neplatný vstup uživatele, jako je chybějící název produktu nebo záporná cena, má za následek výjimku. V [předchozím kurzu](handling-bll-and-dal-level-exceptions-vb.md) jsme prozkoumali, jak přidat kód pro zpracování výjimek do obslužné rutiny události `UpdateCommand` DataList s, aby se zachytává a korektně zobrazovala informace o všech vyvolaných výjimkách. V ideálním případě však rozhraní pro úpravy obsahuje ovládací prvky ověřování, které uživatelům brání v zadávání takových neplatných dat na prvním místě.

V tomto kurzu se dozvíte, jak snadné je přidat ovládací prvky ověřování do `EditItemTemplate` DataList s, aby bylo možné zajistit další foolproof úpravy uživatelského rozhraní. Konkrétně tento kurz používá příklad vytvořený v předchozím kurzu a rozšiřuje rozhraní pro úpravy tak, aby zahrnovalo příslušné ověření.

## <a name="step-1-replicating-the-example-fromhandling-bll--and-dal-level-exceptionshandling-bll-and-dal-level-exceptions-vbmd"></a>Krok 1: replikace příkladu z manipulace s[výjimkami na úrovni knihoven BLL a dal](handling-bll-and-dal-level-exceptions-vb.md)

V kurzu [zpracování výjimek knihoven BLL a dal](handling-bll-and-dal-level-exceptions-vb.md) jsme vytvořili stránku, která uvádí názvy a ceny produktů ve dvou sloupcích upravitelných DataList. Naším cílem tohoto kurzu je rozšířit rozhraní pro úpravy DataList s, aby zahrnovalo ověřovací ovládací prvky. Konkrétně naše logika ověřování bude:

- Vyžadovat, aby byl zadaný název produktu
- Ujistěte se, že zadaná hodnota ceny je platný formát měny.
- Ujistěte se, že hodnota zadaná pro cenu je větší nebo rovna nule, protože záporná hodnota `UnitPrice` je neplatná.

Předtím, než se můžeme podívat na rozšíření předchozího příkladu, aby bylo ověřování zahrnuto, nejdřív je potřeba replikovat příklad ze stránky `ErrorHandling.aspx` ve složce `EditDeleteDataList` na stránku pro tento kurz, `UIValidation.aspx`. Abychom to dosáhli, musíme zkopírovat jak deklarativní značky `ErrorHandling.aspx` stránky, tak i jeho zdrojový kód. Nejdřív zkopírujte přes deklarativní označení provedením následujících kroků:

1. Otevření stránky `ErrorHandling.aspx` v aplikaci Visual Studio
2. Přejděte na deklarativní značku stránky (klikněte na tlačítko zdroj v dolní části stránky).
3. Zkopírujte text v rámci značek `<asp:Content>` a `</asp:Content>` (řádky 3 až 32), jak je znázorněno na obrázku 1.

[![zkopírovat text v &lt;ASP: ovládací prvek Content&gt;](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image2.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image1.png)

**Obrázek 2**: zkopírování textu v ovládacím prvku `<asp:Content>` ([kliknutím zobrazíte obrázek v plné velikosti](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image3.png))

1. Otevřete stránku `UIValidation.aspx`
2. Přejít na deklarativní označení stránky
3. Vložte text do ovládacího prvku `<asp:Content>`.

Chcete-li zkopírovat zdrojový kód, otevřete stránku `ErrorHandling.aspx.vb` a zkopírujte pouze text *v rámci* `EditDeleteDataList_ErrorHandling` třídy. Zkopírujte tři obslužné rutiny události (`Products_EditCommand`, `Products_CancelCommand`a `Products_UpdateCommand`) spolu s metodou `DisplayExceptionDetails`, ale **nekopírujte** deklaraci třídy ani příkazy `using`. Vložte *zkopírovaný text do `EditDeleteDataList_UIValidation` třídy v `UIValidation.aspx.vb`* .

Po přesunutí obsahu a kódu z `ErrorHandling.aspx` na `UIValidation.aspx`chvíli počkejte, než se vyzkouší stránky v prohlížeči. V každé z těchto dvou stránek byste měli vidět stejný výstup a vyzkoušet stejnou funkci (viz obrázek 2).

[![stránka UIValidation. aspx napodobuje funkci v ErrorHandling. aspx.](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image5.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image4.png)

**Obrázek 2**: stránka `UIValidation.aspx` napodobuje funkci v `ErrorHandling.aspx` ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image6.png)

## <a name="step-2-adding-the-validation-controls-to-the-datalist-s-edititemtemplate"></a>Krok 2: Přidání ovládacích prvků ověřování do rozhraní DataList s EditItemTemplate

Při vytváření formulářů pro zadávání dat je důležité, aby uživatelé zadali všechna povinná pole a aby všechny jejich zadané vstupy byly právní a správně formátované hodnoty. Aby bylo zajištěno, že vstupy uživatele jsou platné, ASP.NET poskytuje pět předdefinovaných ověřovacích ovládacích prvků, které jsou navrženy k ověření hodnoty jediného vstupního webového ovládacího prvku:

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) zajistí, že byla zadána hodnota.
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) ověří hodnotu pro jinou hodnotu webového ovládacího prvku nebo konstantní hodnotu nebo zajistí, že formát Value s je platný pro zadaný datový typ.
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) zajišťuje, že hodnota spadá do rozsahu hodnot
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) ověří hodnotu oproti [regulárnímu výrazu](http://en.wikipedia.org/wiki/Regular_expression) .
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) ověří hodnotu podle vlastní uživatelem definované metody

Další informace o těchto pěti ovládacích prvcích odkazují zpátky na kurz [přidávání ověřovacích ovládacích prvků do rozhraní pro úpravy a vkládání](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) , nebo si přečtěte [část ovládací prvky ověřování](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/validation/default.aspx) v kurzu [rychlý Start pro ASP.NET](https://quickstarts.asp.net).

Pro náš kurz budeme muset použít RequiredFieldValidator, aby se zajistilo, že se zadala hodnota pro název produktu, a CompareValidator, aby se zajistilo, že zadaná cena má hodnotu větší nebo rovnu 0 a je prezentována v platném formátu měny.

> [!NOTE]
> Zatímco ASP.NET 1. x má stejné pět ověřovacích ovládacích prvků, ASP.NET 2,0 přináší řadu vylepšení, což je hlavní dvě Podpora skriptů na straně klienta pro prohlížeče kromě aplikace Internet Explorer a možnost rozdělit ovládací prvky ověřování na stránku na skupiny ověření. Další informace o nových funkcích ovládacího prvku ověřování v 2,0 najdete v tématu přeASP.NET [ovládacích prvků ověřování v nástroji 2,0](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx).

Nechte začít přidáním nezbytných ověřovacích ovládacích prvků do `EditItemTemplate`DataList s. Tuto úlohu lze provést prostřednictvím návrháře kliknutím na odkaz Upravit šablony z inteligentní značky DataList s nebo prostřednictvím deklarativní syntaxe. Umožňuje Krokovat s procesem pomocí možnosti Upravit šablony z zobrazení Návrh. Po zvolení úprav `EditItemTemplate`prvku DataList, přidejte objekt RequiredFieldValidator přetažením z panelu nástrojů do rozhraní pro úpravu šablony a umístěte jej za textové pole `ProductName`.

[![přidat RequiredFieldValidator do pole EditItemTemplate za textovým polem NázevVýrobku](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image8.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image7.png)

**Obrázek 3**: přidejte RequiredFieldValidator do `EditItemTemplate After` textového pole `ProductName` ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image9.png)

Všechny ovládací prvky ověřování fungují při ověřování vstupu jednoho ASP.NET webového ovládacího prvku. Proto je potřeba určit, že RequiredFieldValidator, který jsme právě přidali, by měla ověřit proti `ProductName` TextBox; To se provádí nastavením [vlastnosti`ControlToValidate`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) ovládacího prvku pro ověřování na `ID` příslušného webového ovládacího prvku (`ProductName`, v této instanci). Dále nastavte [vlastnost`ErrorMessage`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) na hodnotu musíte zadat název produktu a [vlastnost`Text`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) na \*. Hodnota vlastnosti `Text`, je-li k dispozici, je text, který je zobrazen ovládacím prvkem ověřování v případě, že se ověření nepovede. Hodnota vlastnosti `ErrorMessage`, která je povinná, je používána ovládacím prvkem ovládací souhrnu ověření; Pokud je hodnota vlastnosti `Text` vynechána, zobrazí se ovládací prvek ověřování u neplatného vstupu hodnotu vlastnosti `ErrorMessage`.

Po nastavení těchto tří vlastností RequiredFieldValidator by měla obrazovka vypadat podobně jako na obrázku 4.

[![nastavit vlastnosti RequiredFieldValidator s ControlToValidate, ErrorMessage a text](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image11.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image10.png)

**Obrázek 4**: nastavte vlastnosti RequiredFieldValidator `ControlToValidate`, `ErrorMessage`a `Text` ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image12.png)

Když se RequiredFieldValidator přidá do `EditItemTemplate`, vše zůstává k přidání nezbytného ověření pro textové pole s cenami produktu. Vzhledem k tomu, že `UnitPrice` při úpravách záznamu volitelné, nepotřebujeme přidat RequiredFieldValidator. Je ale potřeba přidat CompareValidator, aby se zajistilo, že `UnitPrice`, pokud je zadaný, je správně naformátovaná jako měna a je větší nebo rovna 0.

Přidejte CompareValidator do `EditItemTemplate` a nastavte jeho vlastnost `ControlToValidate` na `UnitPrice`. jeho vlastnost `ErrorMessage` na hodnotu Price musí být větší než nebo rovna nule a nesmí obsahovat symbol měny a jeho vlastnost `Text` \*. Chcete-li určit, že hodnota `UnitPrice` musí být větší nebo rovna 0, nastavte [vlastnost`Operator`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) CompareValidator s na hodnotu `GreaterThanEqual`, vlastnost [`ValueToCompare`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) na hodnotu 0 a [vlastnost`Type`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) na `Currency`.

Po přidání těchto dvou ovládacích prvků ověřování by měla být deklarativní syntaxe `EditItemTemplate` DataList s vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](adding-validation-controls-to-the-datalist-s-editing-interface-vb/samples/sample1.aspx)]

Po provedení těchto změn otevřete stránku v prohlížeči. Pokud se pokusíte vynechat název nebo zadat neplatnou hodnotu ceny při úpravě produktu, zobrazí se vedle textového pole hvězdička. Jak ukazuje obrázek 5, hodnota ceny zahrnující symbol měny, jako je například $19,95, se považuje za neplatnou. CompareValidator s `Currency` `Type` umožňuje oddělovač číslic (například čárky nebo tečky, v závislosti na nastavení jazykové verze) a úvodní znaménko plus nebo mínus, ale *nepovoluje symbol* měny. Toto chování může perplex uživatele, protože rozhraní pro úpravy aktuálně vykresluje `UnitPrice` pomocí formátu měny.

[![se zobrazí hvězdička vedle textových polí s neplatným vstupem.](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image14.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image13.png)

**Obrázek 5**: u textových polí s neplatným vstupem se zobrazí hvězdička ([kliknutím zobrazíte obrázek v plné velikosti](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image15.png)).

I když ověřování funguje tak, jak je, uživatel musí při úpravách záznamu ručně odebrat symbol měny, což není přijatelné. Kromě toho, pokud existují neplatné vstupy v rozhraní pro úpravy, tlačítka aktualizovat ani zrušit, když kliknou, vyvolá zpětné odeslání. V ideálním případě tlačítko Storno vrátí prvek DataList do stavu před úpravou bez ohledu na platnost vstupů uživatele. Před aktualizací informací o produktu v obslužné rutině události `UpdateCommand` DataList je také potřeba zajistit, aby data stránky byla platná, protože ověřování pomocí logiky na straně klienta může být obcházeno uživateli, jejichž prohlížeče buď nepodporují JavaScript, nebo mají zakázanou podporu.

## <a name="removing-the-currency-symbol-from-the-edititemtemplate-s-unitprice-textbox"></a>Odebrání symbolu měny z pole EditItemTemplate s UnitPrice

Při použití `Currency``Type`CompareValidator s nesmí vstup ověřený, obsahovat žádné symboly měny. Přítomnost takových symbolů způsobí, že CompareValidator označí vstup jako neplatný. Naše rozhraní pro úpravy však v současnosti obsahuje symbol měny v textovém poli `UnitPrice`, což znamená, že uživatel musí explicitně odebrat symbol měny před uložením změn. K nápravě máme tři možnosti:

1. Nakonfigurujte `EditItemTemplate` tak, aby hodnota `UnitPrice` TextBox neformátovala jako měna.
2. Umožní uživateli zadat symbol měny odebráním CompareValidator a jeho nahrazením RegularExpressionValidator, který kontroluje správně formátovanou hodnotu měny. Zde je uvedeno, že regulární výraz pro ověření hodnoty měny není stejně jednoduchý jako CompareValidator a by vyžadoval psaní kódu, pokud jsme chtěli začlenit nastavení jazykové verze.
3. Odeberte ovládací prvek ověřování zcela a spoléhat na vlastní logiku ověřování na straně serveru v prvku GridView `RowUpdating` obslužná rutina události.

Pro tento kurz si podíváme s možností 1. V současné době je `UnitPrice` formátován jako hodnota měny z důvodu výrazu datové vazby pro textové pole v `EditItemTemplate`: `<%# Eval("UnitPrice", "{0:c}") %>`. Změňte příkaz `Eval` na `Eval("UnitPrice", "{0:n2}")`, který formátuje výsledek jako číslo se dvěma číslicemi přesnosti. To lze provést přímo prostřednictvím deklarativní syntaxe nebo kliknutím na odkaz Upravit datové vazby z `UnitPrice` textového pole v `EditItemTemplate`DataList s.

V důsledku této změny formátovaná cena v rozhraní pro úpravy zahrnuje čárky jako oddělovač skupin a tečku jako oddělovač desetinných míst, ale ponechá symbol měny.

> [!NOTE]
> Když odeberete formát měny z upravitelného rozhraní, zjistíte, že je vhodné vložit symbol měny jako text mimo textové pole. Slouží jako pomocný parametr pro uživatele, že nemusejí zadávat symbol měny.

## <a name="fixing-the-cancel-button"></a>Oprava tlačítka Storno

Ve výchozím nastavení ověřování webové ovládací prvky generuje JavaScript k provedení ověření na straně klienta. Při kliknutí na tlačítko, LinkButton nebo obrázkové, jsou ovládací prvky ověřování na stránce zkontrolovány na straně klienta před tím, než dojde k postbacku. Pokud jsou k dispozici neplatná data, zpětné volání je zrušeno. U některých tlačítek je ale možné, že platnost dat neklade; v takovém případě je zrušení zpětného volání z důvodu neplatných dat rušivé.

Tlačítko Zrušit je takový příklad. Představte si, že uživatel zadá neplatná data, jako je například vynechání názvu produktu, a pak rozhodne, že nechce produkt po celou hodnotu uložit, a narazí na tlačítko Storno. V současné době tlačítko zrušit aktivuje ovládací prvky ověřování na stránce, která hlásí, že chybí název produktu, a brání zpětnému odeslání. Náš uživatel musí zadat nějaký text do textového pole `ProductName` jenom pro zrušení procesu úprav.

Naštěstí, tlačítko, LinkButton a obrázkové mají [vlastnost`CausesValidation`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.causesvalidation.aspx) , která může indikovat, zda kliknutí na tlačítko má zahájit logiku ověřování (výchozí nastavení `True`). Nastavte vlastnost `CausesValidation` tlačítka Storno na hodnotu `False`.

## <a name="ensuring-the-inputs-are-valid-in-the-updatecommand-event-handler"></a>Zajištění platnosti vstupů v obslužné rutině události UpdateCommand

Z důvodu skriptu na straně klienta generovaného ovládacími prvky ověřování, pokud uživatel zadá neplatný vstup, zruší všechny postbacky iniciované pomocí tlačítka, LinkButton nebo obrázkové, jejichž vlastnosti `CausesValidation` jsou `True` (výchozí). Pokud se ale uživatel navštíví s prohlížečem antiquated nebo s tím, jehož podpora JavaScriptu je zakázaná, nespustí se kontroly ověřování na straně klienta.

Všechny ovládací prvky ověřování ASP.NET zopakují svůj ověřovací logiku ihned po zpětném odeslání a nahlásí celkovou platnost vstupů stránky prostřednictvím [vlastnosti`Page.IsValid`](https://msdn.microsoft.com/library/system.web.ui.page.isvalid.aspx). Tok stránky ale není nijak přerušený ani zastavený podle hodnoty `Page.IsValid`. Jako vývojáři je naše zodpovědnost za zajištění, že vlastnost `Page.IsValid` má hodnotu `True` před pokračováním v kódu, který předpokládá platná vstupní data.

Pokud je na uživateli zakázaný JavaScript, navštíví naši stránku, upraví produkt, zadá cenu za moc nákladný a klikne na tlačítko Aktualizovat, ověřování na straně klienta se obejít a postback se následovat. Při zpětném volání se spustí obslužná rutina ASP.NET stránky s `UpdateCommand` a při pokusu o analýzu příliš nákladného na `Decimal`je vyvolána výjimka. Vzhledem k tomu, že máme zpracování výjimek, taková výjimka bude zpracována řádným, ale můžeme zabránit tomu, aby se neplatná data procházela v prvním místě, a to tak, že bude pokračovat pouze s `UpdateCommand` obslužnou rutinou události, pokud `Page.IsValid` má hodnotu `True`.

Přidejte následující kód na začátek obslužné rutiny události `UpdateCommand` těsně před blok `Try`:

[!code-vb[Main](adding-validation-controls-to-the-datalist-s-editing-interface-vb/samples/sample2.vb)]

S tímto sčítáním se produkt pokusí aktualizovat jenom v případě, že jsou odeslaná data platná. Většina uživatelů nebude moci odeslat neplatná data z důvodu ověřování skriptů na straně klienta, ale uživatelé, jejichž prohlížeče nepodporují JavaScript nebo které mají zakázanou podporu JavaScriptu, mohou obejít kontroly na straně klienta a odesílat neplatná data.

> [!NOTE]
> Čtecí modul bystří si odvolá, že při aktualizaci dat pomocí prvku GridView, nemuseli byste explicitně kontrolovat vlastnost `Page.IsValid` v naší třídě Code-on na pozadí. Je to proto, že prvek GridView aktualizuje vlastnost `Page.IsValid` pro nás a pokračuje pouze s aktualizací pouze v případě, že vrací hodnotu `True`.

## <a name="step-3-summarizing-data-entry-problems"></a>Krok 3: sumarizace problémů se zadáváním dat

Kromě pěti ovládacích prvků ověřování obsahuje ASP.NET [ovládací prvek ovládací souhrnu ověření](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx), který zobrazuje `ErrorMessage` s těmito ověřovacími ovládacími prvky, které zjistila neplatná data. Tato souhrnná data lze zobrazit jako text na webové stránce nebo modálním objektem MessageBox na straně klienta. Tento kurz vám usnadní zahrnutí MessageBox na straně klienta, které shrnuje jakékoli problémy s ověřením.

Chcete-li to provést, přetáhněte ovládací prvek ovládací souhrnu ověření z panelu nástrojů na Návrhář. Poloha ovládacího prvku ovládací souhrnu ověření má nezávisle na skutečnosti, protože ho znovu nakonfigurujeme tak, aby zobrazoval pouze souhrn jako MessageBox. Po přidání ovládacího prvku nastavte jeho [vlastnost`ShowSummary`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) na `False` a jeho [vlastnost`ShowMessageBox`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) na `True`. S tímto sčítáním jsou všechny chyby ověřování shrnuty na straně klienta MessageBox (viz obrázek 6).

[![chyby ověřování jsou shrnuty ve MessageBox na straně klienta.](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image17.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image16.png)

**Obrázek 6**: Chyby ověřování jsou shrnuty v prvku MessageBox na straně klienta ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image18.png)

## <a name="summary"></a>Přehled

V tomto kurzu jsme zjistili, jak snížit pravděpodobnost výjimek pomocí ověřovacích ovládacích prvků, abyste proaktivně zajistili, že vstupy uživatelů jsou platné před pokusem o jejich použití v pracovním postupu aktualizace. ASP.NET poskytuje pět ověřovacích webových ovládacích prvků, které jsou navrženy pro kontrolu konkrétního vstupu webového ovládacího prvku a hlášení o platnosti vstupu s. V tomto kurzu jsme použili dvě z těchto pěti ovládacích prvků RequiredFieldValidator a CompareValidator, abyste zajistili, že byl dodán název produktu a že cena měla formát měny s hodnotou větší než nebo rovna nule.

Přidávání ověřovacích ovládacích prvků do rozhraní pro úpravy DataList s je tak jednoduché jako přetahování na `EditItemTemplate` ze sady nástrojů a nastavení několik vlastností. Ve výchozím nastavení ovládací prvky ověřování automaticky generují skript ověřování na straně klienta; poskytují také ověřování na straně serveru při postbacku a ukládají kumulativní výsledek do vlastnosti `Page.IsValid`. Chcete-li při kliknutí na tlačítko, LinkButton nebo obrázkové obejít ověřování na straně klienta, nastavte vlastnost tlačítko s `CausesValidation` na `False`. Před provedením jakýchkoli úkolů s daty odeslanými při zpětném volání ověřte také, že vlastnost `Page.IsValid` vrátí `True`.

Všechny kurzy pro úpravy DataList, které jsme dosud zkoumali, mají velmi jednoduchá rozhraní pro úpravy a textové pole pro název produktu a další pro tuto cenu. Rozhraní pro úpravy však může obsahovat kombinaci různých webových ovládacích prvků, jako jsou například DropDownList, kalendáře, přepínače, zaškrtávací políčka a tak dále. V našem dalším kurzu se podíváme na sestavení rozhraní, které používá různé webové ovládací prvky.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Dennis Patterson, Ken Pespisa a Liz Shulok. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](handling-bll-and-dal-level-exceptions-vb.md)
> [Další](customizing-the-datalist-s-editing-interface-vb.md)

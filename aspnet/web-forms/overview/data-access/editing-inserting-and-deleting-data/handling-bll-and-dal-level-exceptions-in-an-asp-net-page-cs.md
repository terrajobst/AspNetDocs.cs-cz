---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs
title: Zpracování výjimek na úrovni knihoven BLL-a DAL na stránce ASP.NET (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se dozvíte, jak zobrazit přívětivou a informativní chybovou zprávu, která by během operace vložení, aktualizace nebo odstranění mohla nastat výjimka...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 49d8a66c-3ea8-4087-839f-179d1d94512a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 2b9cdb5af6f33171b191d5a80473c7796eb098d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78608386"
---
# <a name="handling-bll--and-dal-level-exceptions-in-an-aspnet-page-c"></a>Zpracování výjimek na úrovni knihoven BLL a DAL na stránce ASP.NET (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_18_CS.exe) nebo [Stáhnout PDF](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/datatutorial18cs1.pdf)

> V tomto kurzu se dozvíte, jak zobrazit přívětivou a informativní chybovou zprávu, pokud se během operace vložení, aktualizace nebo odstranění webového ovládacího prvku ASP.NET data vyskytla výjimka.

## <a name="introduction"></a>Úvod

Práce s daty z webové aplikace v ASP.NET s využitím vícevrstvé architektury aplikace zahrnuje následující tři obecné kroky:

1. Určete, jaká metoda vrstvy obchodní logiky musí být vyvolána a jaké hodnoty parametrů se mají předat. Hodnoty parametrů můžou být pevně kódované, programově přiřazené nebo vstupy zadané uživatelem.
2. Vyvolat metodu.
3. Zpracování výsledků. Při volání metody knihoven BLL, která vrací data, může to zahrnovat vázání dat na webový ovládací prvek dat. Pro metody knihoven BLL, které mění data, to může zahrnovat provedení některé akce na základě návratové hodnoty nebo řádného zpracování jakékoli výjimky, která vznikla v kroku 2.

Jak jsme viděli v [předchozím kurzu](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md), ovládací prvky ObjectDataSource a data webového ovládacího prvku poskytují body rozšiřitelnosti pro kroky 1 a 3. Prvek GridView, například aktivuje jeho událost `RowUpdating` před přiřazením jeho hodnot polí do kolekce `UpdateParameters` prvku ObjectDataSource; jeho událost `RowUpdated` je vyvolána poté, co prvek ObjectDataSource dokončí operaci.

Již jsme prozkoumali události, které se aktivují v kroku 1, a zjistili jste, jak je lze použít k přizpůsobení vstupních parametrů nebo zrušení operace. V tomto kurzu provedeme upozornění na události, které se aktivují po dokončení operace. Pomocí těchto obslužných rutin událostí na úrovni post můžeme mimo jiné zjistit, jestli během operace došlo k výjimce, a nemusíte ji řádně napravit a zobrazovat na obrazovce přívětivou, informativní chybovou zprávu, a to než výchozí ASP.NET. Stránka výjimky.

Pro ilustraci práce s těmito událostmi po úrovních vytvoříme stránku, která obsahuje seznam produktů v upravitelném prvku GridView. Pokud při aktualizaci produktu dojde k výjimce, zobrazí se na stránce ASP.NET krátká zpráva nad prvku GridView, což vysvětluje, že došlo k problému. Pojďme začít!

## <a name="step-1-creating-an-editable-gridview-of-products"></a>Krok 1: vytvoření upravitelného prvku GridView u produktů

V předchozím kurzu jsme vytvořili upravitelný prvek GridView s pouze dvěma poli `ProductName` a `UnitPrice`. To vyžadovalo vytvoření dalšího přetížení pro metodu `UpdateProduct` `ProductsBLL` třídy, jednu, která přijala pouze tři vstupní parametry (název produktu, Jednotková cena a ID), a to na rozdíl od parametru pro každé pole produktu. Pro tento kurz Pojďme tuto techniku znovu vymezit vytvořením upravitelného prvku GridView, který zobrazuje název produktu, množství na jednotku, cenu za jednotku a jednotky na skladě, ale umožňuje upravovat jenom název, jednotkovou cenu a jednotky na skladě.

Aby bylo možné tento scénář přizpůsobit, budete potřebovat další přetížení metody `UpdateProduct`, jednu, která přijímá čtyři parametry: název produktu, Jednotková cena, jednotky na skladě a ID. Do třídy `ProductsBLL` přidejte následující metodu:

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample1.cs)]

Po dokončení této metody jsme připraveni vytvořit stránku ASP.NET, která umožňuje úpravu těchto čtyř konkrétních polí produktu. Otevřete stránku `ErrorHandling.aspx` ve složce `EditInsertDelete` a přidejte prvek GridView do stránky pomocí návrháře. Vytvořte vazby na prvek GridView k novému prvku ObjectDataSource, mapování `Select()` metody na metodu `GetProducts()` `ProductsBLL` třídy a metodu `Update()` na `UpdateProduct` přetížení, které jste právě vytvořili.

[![použít přetížení metody UpdateProduct, které přijímá čtyři vstupní parametry.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image2.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image1.png)

**Obrázek 1**: použití přetížení metody `UpdateProduct`, které přijímá čtyři vstupní parametry ([kliknutím zobrazíte obrázek v plné velikosti).](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image3.png)

Tím se vytvoří prvek ObjectDataSource s kolekcí `UpdateParameters` se čtyřmi parametry a GridView s polem pro každé pole produktu. Deklarativní označení prvku ObjectDataSource přiřadí vlastnost `OldValuesParameterFormatString` hodnotu `original_{0}`, která způsobí výjimku, protože naše třída knihoven BLL neočekává, že vstupní parametr s názvem `original_productID` má být předán. Nezapomeňte odebrání tohoto nastavení zcela odebrat z deklarativní syntaxe (nebo ho nastavte na výchozí hodnotu `{0}`).

Potom zredukovali dolů v prvku GridView, aby zahrnovala pouze `ProductName`, `QuantityPerUnit`, `UnitPrice`a `UnitsInStock` BoundFields. Také můžete použít jakékoli formátování na úrovni pole, které považujete za nutné (například změna vlastností `HeaderText`).

V předchozím kurzu jsme se podívali na způsob formátování `UnitPrice` vlastnost BoundField jako měny v režimu jen pro čtení a v režimu úprav. Pojďme to udělat tady. Vystavte si, že toto nastavení vlastnosti `DataFormatString` vlastnost BoundField na `{0:c}`, jeho vlastnost `HtmlEncode` na `false`a jeho `ApplyFormatInEditMode` na `true`, jak je znázorněno na obrázku 2.

[![nakonfigurovat vlastnost BoundField UnitPrice, který se má zobrazit jako měna](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image5.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image4.png)

**Obrázek 2**: Konfigurace `UnitPrice` vlastnost BoundField, která se má zobrazit jako měna ([kliknutím zobrazíte obrázek v plné velikosti](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image6.png))

Formátování `UnitPrice` jako měny v rozhraní pro úpravy vyžaduje vytvoření obslužné rutiny události pro událost `RowUpdating` prvku GridView, která analyzuje řetězec ve formátu měny na hodnotu `decimal`. Odvolat, zda `RowUpdating` obslužná rutina události z posledního kurzu zkontrolována, zda uživatel zadal hodnotu `UnitPrice`. V tomto kurzu ale umožníte uživateli vynechat tuto cenu.

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample2.cs)]

Náš prvek GridView obsahuje `QuantityPerUnit` vlastnost BoundField, ale tento vlastnost BoundField by měl být pouze pro účely zobrazení a uživatel by neměl být upravitelný. Pokud to chcete uspořádat, jednoduše nastavte vlastnost `ReadOnly` BoundFields na `true`.

[![nastavit QuantityPerUnit vlastnost BoundField jen pro čtení](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image8.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image7.png)

**Obrázek 3**: nastavte `QuantityPerUnit` vlastnost BoundField jen pro čtení ([kliknutím zobrazíte obrázek v plné velikosti).](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image9.png)

Nakonec zaškrtněte políčko Povolit úpravy z inteligentní značky GridView. Po dokončení těchto kroků by měl Návrhář `ErrorHandling.aspx` stránky vypadat podobně jako obrázek 4.

[![odebrat všechny kromě požadovaných BoundFields a zaškrtnout políčko Povolit úpravy.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image11.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image10.png)

**Obrázek 4**: Odeberte všechna kromě potřebná BoundFields a zaškrtněte políčko Povolit úpravy ([kliknutím zobrazíte obrázek v plné velikosti).](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image12.png)

V tuto chvíli máme seznam všech produktů ' `ProductName`, `QuantityPerUnit`, `UnitPrice`a `UnitsInStock` polí; je však možné upravovat pouze pole `ProductName`, `UnitPrice`a `UnitsInStock`.

[![uživatelé teď můžou snadno upravovat názvy, ceny a jednotky produktů v uložených polích.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image14.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image13.png)

**Obrázek 5**: uživatelé teď můžou snadno upravovat názvy, ceny a jednotky produktů v uložených polích ([kliknutím zobrazíte obrázek v plné velikosti](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image15.png)).

## <a name="step-2-gracefully-handling-dal-level-exceptions"></a>Krok 2: řádné zpracování výjimek na úrovni DAL

I když náš upravitelný GridView funguje, když uživatelé zadají právní hodnoty pro název upravovaného produktu, cenu a jednotky na skladě, a zadáním neplatných hodnot způsobí výjimku. Například vynechání hodnoty `ProductName` způsobí vyvolání [NoNullAllowedException](https://msdn.microsoft.com/library/default.asp?url=/library/cpref/html/frlrfsystemdatanonullallowedexceptionclasstopic.asp) , protože vlastnost `ProductName` ve třídě `ProductsRow` má vlastnost `AllowDBNull` nastavenou na `false`; Pokud je databáze mimo provoz, při pokusu o připojení k databázi vygeneruje služba TableAdapter `SqlException`. Bez provedení jakékoli akce se tyto výjimky doplní z vrstvy přístupu k datům do vrstvy obchodní logiky, pak na stránku ASP.NET a nakonec do modulu runtime ASP.NET.

V závislosti na tom, jak je vaše webová aplikace nakonfigurovaná a jestli nedošlo k aplikaci `localhost`, může mít Neošetřená výjimka buď obecný server – chybovou stránku, podrobnou zprávu o chybě nebo uživatelsky přívětivou webovou stránku. Další informace o tom, jak modul runtime ASP.NET reaguje na nezachycenou výjimku, najdete v tématu [zpracování chyb webové aplikace v ASP.NET](http://www.15seconds.com/issue/030102.htm) a [elementu customErrors](https://msdn.microsoft.com/library/h0hfz6fc(VS.80).aspx) .

Obrázek 6 zobrazuje obrazovku zjištěné při pokusu o aktualizaci produktu bez zadání `ProductName` hodnoty. Toto je výchozí podrobná zpráva o chybách, která se zobrazí, když připravujete prostřednictvím `localhost`.

[![vynechání názvu produktu zobrazí podrobnosti o výjimce.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image17.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image16.png)

**Obrázek 6**: vynechání názvu produktu zobrazí podrobnosti o výjimce ([kliknutím zobrazíte obrázek v plné velikosti).](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image18.png)

I když jsou informace o výjimce užitečné při testování aplikace, předvádí se koncovému uživateli s takovou obrazovkou, která je v tváři výjimky, méně než ideální. Koncový uživatel pravděpodobně neví, co je `NoNullAllowedException` nebo proč to bylo způsobeno. Lepším řešením je prezentovat uživatele více uživatelsky přívětivými zprávami s vysvětlením, že při pokusu o aktualizaci produktu došlo k potížím.

Pokud při provádění operace dojde k výjimce, události na úrovni post v prvku ObjectDataSource i v ovládacím prvku data web poskytují způsob, jak je rozpoznat a zrušit výjimku z šíření až do modulu runtime ASP.NET. V našem příkladu vytvoříme obslužnou rutinu události pro událost `RowUpdated` prvku GridView, která určuje, zda byla vyvolána výjimka, a pokud ano, zobrazí podrobnosti o výjimce v ovládacím prvku web Label.

Začněte přidáním popisku na stránku ASP.NET a nastavením jeho vlastnosti `ID` na `ExceptionDetails` a vymažte jeho vlastnost `Text`. Aby bylo možné nakreslit uživatele na tuto zprávu, nastavte jeho vlastnost `CssClass` na `Warning`, což je Třída CSS, kterou jsme přidali do souboru `Styles.css` v předchozím kurzu. Odvolání této třídy CSS způsobí, že se text popisku zobrazí červeně, kurzívou, tučně a extra velkým písmem.

[![přidání webového ovládacího prvku popisek na stránku](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image20.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image19.png)

**Obrázek 7**: Přidání webového ovládacího prvku popisek na stránku ([kliknutím zobrazíte obrázek v plné velikosti](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image21.png))

Vzhledem k tomu, že chceme, aby byl tento ovládací prvek web popisku viditelný pouze ihned po výskytu výjimky, nastavte jeho vlastnost `Visible` na hodnotu false v obslužné rutině události `Page_Load`:

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample3.cs)]

U tohoto kódu na první návštěvě stránky a následných postbackech má ovládací prvek `ExceptionDetails` nastavenou vlastnost `Visible` nastavenou na `false`. V tváři výjimky na úrovni DAL nebo knihoven BLL, která se dá rozpoznat v obslužné rutině události `RowUpdated` prvku GridView, nastavíme vlastnost `Visible` ovládacího prvku `ExceptionDetails` na hodnotu true. Vzhledem k tomu, že se obslužné rutiny událostí webového ovládacího prvku vyskytují po obslužné rutině `Page_Load` události v životním cyklu stránky, bude zobrazen popisek. Při příštím postbacku však obslužná rutina události `Page_Load` vrátí vlastnost `Visible` zpět do `false`a skryje ji ze zobrazení znovu.

> [!NOTE]
> Případně je možné odebrat nutnost nastavení vlastnosti `Visible` ovládacího prvku `ExceptionDetails` v `Page_Load` přiřazením jeho `Visible` vlastnosti `false` v deklarativní syntaxi a zakázáním jeho stavu zobrazení (nastavením vlastnosti `EnableViewState` na `false`). Tento alternativní postup budeme používat v budoucím kurzu.

Při přidání ovládacího prvku popisek je dalším krokem vytvoření obslužné rutiny události pro událost `RowUpdated` prvku GridView. Vyberte prvek GridView v návrháři, přejděte na okno Vlastnosti a klikněte na ikonu blesku a uveďte události prvku GridView. Již by měla existovat položka pro událost `RowUpdating` prvku GridView, protože jsme vytvořili obslužnou rutinu události pro tuto událost dříve v tomto kurzu. Vytvořte také obslužnou rutinu události pro událost `RowUpdated`.

![Vytvoření obslužné rutiny události pro událost RowUpdated metody Update prvku GridView](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image22.png)

**Obrázek 8**: vytvoření obslužné rutiny události pro událost `RowUpdated` prvku GridView

> [!NOTE]
> Můžete také vytvořit obslužnou rutinu události prostřednictvím rozevíracích seznamů v horní části souboru třídy kódu na pozadí. V rozevíracím seznamu na levé straně vyberte prvek GridView a událost `RowUpdated` z pravé části.

Vytvořením této obslužné rutiny události se přidá následující kód do třídy kódu na pozadí stránky ASP.NET:

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample4.cs)]

Tento druhý vstupní parametr obslužné rutiny události je objekt typu [GridViewUpdatedEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdatedeventargs.aspx), který má tři vlastnosti zájmu pro zpracování výjimek:

- `Exception` odkaz na vyvolanou výjimku; Pokud nebyla vyvolána žádná výjimka, bude mít tato vlastnost hodnotu `null`
- `ExceptionHandled` logickou hodnotu, která označuje, zda byla výjimka zpracována v obslužné rutině události `RowUpdated`; Pokud `false` (výchozí), výjimka se znovu vyvolá percolating až do ASP.NET runtime
- `KeepInEditMode` Pokud je nastavená na `true` upravený řádek prvku GridView zůstane v režimu úprav; Pokud `false` (výchozí), řádek GridView se vrátí zpět do režimu jen pro čtení.

Náš kód, poté, by měl ověřit, zda `Exception` není `null`, což znamená, že při provádění této operace byla vyvolána výjimka. V takovém případě chceme:

- Zobrazit uživatelsky přívětivou zprávu v popisku `ExceptionDetails`
- Označení, že byla výjimka zpracována
- Ponechat řádek GridView v režimu úprav

Následující kód dosahuje těchto cílů:

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample5.cs)]

Tato obslužná rutina události začíná kontrolou, zda `e.Exception` `null`. Pokud není, vlastnost `Visible` popisku `ExceptionDetails` je nastavená na `true` a vlastnost `Text` na hodnotu došlo k potížím s aktualizací produktu. Podrobnosti o skutečné výjimce, která byla vyvolána, je uložena ve vlastnosti `InnerException` objektu `e.Exception`. Tato vnitřní výjimka je prověřena a pokud má konkrétní typ, připojí se k vlastnosti `Text` `ExceptionDetails` popisku Další, užitečná zpráva. A konečně vlastnosti `ExceptionHandled` a `KeepInEditMode` jsou nastaveny na `true`.

Obrázek 9 ukazuje snímek obrazovky této stránky při vynechání názvu produktu. Obrázek 10 zobrazuje výsledky při zadání neplatné hodnoty `UnitPrice` (-50).

[![NázevVýrobku vlastnost BoundField musí obsahovat hodnotu.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image24.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image23.png)

**Obrázek 9**: `ProductName` vlastnost BoundField musí obsahovat hodnotu ([kliknutím zobrazíte obrázek v plné velikosti](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image25.png)).

[![záporné hodnoty UnitPrice nejsou povolené.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image27.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image26.png)

**Obrázek 10**: záporné hodnoty `UnitPrice` nejsou povoleny ([kliknutím zobrazíte obrázek v plné velikosti).](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image28.png)

Nastavením vlastnosti `e.ExceptionHandled` na `true`, obslužná rutina `RowUpdated` události označila, že zpracovala výjimku. Proto výjimka nebude šířit až do modulu runtime ASP.NET.

> [!NOTE]
> Obrázky 9 a 10 znázorňují řádný způsob, jak zpracovat výjimky způsobené neplatným uživatelským vstupem. V ideálním případě by se tento neplatný vstup nikdy nedostal do vrstvy obchodní logiky na prvním místě, protože před vyvoláním metody `UpdateProduct` `ProductsBLL` třídy by se měla ověřit, jestli jsou vstupy uživatele platné. V našem dalším kurzu se dozvíte, jak přidat ověřovací ovládací prvky do rozhraní pro úpravy a vkládání, aby se zajistilo, že data odeslaná do vrstvy obchodní logiky odpovídají obchodním pravidlům. Ověřování ovládací prvky nebrání pouze vyvolání metody `UpdateProduct`, dokud nejsou platná uživatelem zadaná data, ale také poskytují více informativní uživatelské prostředí pro identifikaci problémů se zadáváním dat.

## <a name="step-3-gracefully-handling-bll-level-exceptions"></a>Krok 3: řádné zpracování výjimek na úrovni knihoven BLL

Při vkládání, aktualizaci nebo odstraňování dat může vrstva přístupu k datům vyvolat výjimku na straně chyby související s daty. Databáze je možná offline, požadovaný sloupec databázové tabulky pravděpodobně nemá zadanou hodnotu nebo omezení na úrovni tabulky bylo porušeno. Kromě striktních výjimek souvisejících s daty může vrstva obchodní logiky použít výjimky, které označují, kdy byla porušena obchodní pravidla. V kurzu [Vytvoření vrstvy obchodní logiky](../introduction/creating-a-business-logic-layer-cs.md) jste například přidali kontrolu obchodního pravidla do původního `UpdateProduct` přetížení. Konkrétně Pokud uživatel označí produkt jako vyřazený, vyžadujeme, aby tento produkt nebyl jediným poskytovatelem poskytovaným jeho dodavatelem. Pokud tato podmínka byla narušena, `ApplicationException` byla vyvolána.

Pro `UpdateProduct` přetížení vytvořené v tomto kurzu přidáme obchodní pravidlo, které zabrání nastavení `UnitPrice` pole na novou hodnotu, která je větší než dvojnásobek původní `UnitPrice` hodnoty. Chcete-li toho dosáhnout, upravte `UpdateProduct` přetížení tak, že provede tuto kontrolu a vyvolá `ApplicationException`, pokud je pravidlo porušeno. Následující aktualizovaná metoda:

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/samples/sample6.cs)]

Tato změna způsobí, že jakákoli aktualizace ceny, která je více než dvojnásobek stávající ceny, vygeneruje `ApplicationException`. Stejně jako výjimka vyvolaná z DAL, tato knihoven BLLá `ApplicationException` může být zjištěna a zpracována v obslužné rutině události `RowUpdated` prvku GridView. Ve skutečnosti kód obslužné rutiny události `RowUpdated` jako napsaný, správně detekuje tuto výjimku a zobrazí hodnotu vlastnosti `Message` `ApplicationException`. Obrázek 11 znázorňuje snímek obrazovky, když se uživatel pokusí aktualizovat cenu hodnoty Chai na $50,00, což je více než dvojnásobek aktuální ceny $19,95.

[![obchodních pravidel zakáže ceny zvýšení ceny za více než dvojnásobek ceny produktu.](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image30.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image29.png)

**Obrázek 11**: obchodní pravidla neumožňují zvýšení ceny za více než dvojnásobek ceny produktu ([kliknutím zobrazíte obrázek v plné velikosti).](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs/_static/image31.png)

> [!NOTE]
> V ideálním případě by se pravidla obchodní logiky refaktoroval z přetížení `UpdateProduct` metody a do společné metody. Tento postup je ponechán jako cvičení pro čtenáře.

## <a name="summary"></a>Souhrn

Během vkládání, aktualizace a odstraňování operací se webový ovládací prvek dat i prvek ObjectDataSource účastní událostí před a na úrovni, které zastavují skutečnou operaci. Jak jsme viděli v tomto kurzu a předchozí, při práci s upravitelným ovládacím prvkem GridView `RowUpdating` událost prvku GridView, následovanou událostmi `Updating` elementu ObjectDataSource, v níž je příkaz Update proveden na podkladovém objektu ObjectDataSource. Po dokončení operace se aktivuje událost `Updated` ObjectDataSource a za ní následuje událost `RowUpdated` prvku GridView.

Můžeme vytvořit obslužné rutiny událostí pro události před úrovní, aby bylo možné přizpůsobit vstupní parametry nebo události na úrovni po, aby bylo možné kontrolovat výsledky operace a reagovat na ně. Obslužné rutiny události po úrovni se nejčastěji používají k detekci, zda během operace došlo k výjimce. Na přední straně výjimky mohou tyto obslužné rutiny události na úrovni, volitelně zpracovat výjimku na své vlastní. V tomto kurzu jsme zjistili, jak takovou výjimku zvládnout zobrazením popisné chybové zprávy.

V dalším kurzu se dozvíte, jak snížit pravděpodobnost výjimek vyplývajících z potíží s formátováním dat (například zadáním záporné `UnitPrice`). Konkrétně se podíváme na postup přidání ověřovacích ovládacích prvků do rozhraní pro úpravy a vkládání.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Liz Shulok. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
> [Další](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)

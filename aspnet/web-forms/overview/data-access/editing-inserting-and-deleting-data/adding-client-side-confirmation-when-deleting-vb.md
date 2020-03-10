---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb
title: Přidání potvrzení na straně klienta při odstraňování (VB) | Microsoft Docs
author: rick-anderson
description: V rozhraních, které jsme doposud vytvořili, může uživatel omylem odstranit data kliknutím na tlačítko Odstranit, když chtějí kliknout na tlačítko Upravit. V této t...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 6331e02e-c465-4cdf-bd3f-f07680c289d6
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: addb5a1fdc5793309388c5f06b44fb3b145bc102
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78610514"
---
# <a name="adding-client-side-confirmation-when-deleting-vb"></a>Přidání potvrzení odstranění na straně klienta (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_VB.exe) nebo [Stáhnout PDF](adding-client-side-confirmation-when-deleting-vb/_static/datatutorial22vb1.pdf)

> V rozhraních, které jsme doposud vytvořili, může uživatel omylem odstranit data kliknutím na tlačítko Odstranit, když chtějí kliknout na tlačítko Upravit. V tomto kurzu přidáme potvrzovací dialog na straně klienta, který se zobrazí po kliknutí na tlačítko pro odstranění.

## <a name="introduction"></a>Úvod

V posledních několika kurzech jsme se seznámili s tím, jak používat naši architekturu aplikace, prvek ObjectDataSource a datově webové ovládací prvky, které poskytují funkce pro vkládání, úpravy a odstraňování. Odstranění rozhraní, které jsme zkoumali, jsme doposud sestavili pomocí tlačítka odstranit, které po kliknutí způsobí postback a vyvolá metodu ObjectDataSource `Delete()`. Metoda `Delete()` potom vyvolá nakonfigurovanou metodu z vrstvy obchodní logiky, která rozšíří volání dolů do vrstvy přístupu k datům, a vydává v databázi skutečný příkaz `DELETE`.

Toto uživatelské rozhraní sice umožňuje návštěvníkům odstraňovat záznamy prostřednictvím ovládacích prvků GridView, DetailsView nebo FormView, ale nemá žádné řazení potvrzení, když uživatel klikne na tlačítko Odstranit. Pokud uživatel omylem klikne na tlačítko Odstranit, když chtějí kliknout na upravit, místo toho se odstraní záznam, který chtěl aktualizovat. Aby k tomu nedocházelo, v tomto kurzu přidáme potvrzovací dialog na straně klienta, který se zobrazí po kliknutí na tlačítko pro odstranění.

Funkce `confirm(string)` JavaScriptu zobrazí svůj vstupní parametr řetězce jako text uvnitř modálního dialogového okna, které je vybavené dvěma tlačítky-OK a zrušit (viz obrázek 1). Funkce `confirm(string)` vrací logickou hodnotu v závislosti na tlačítku, na které je kliknuto (`true`, pokud uživatel klikne na tlačítko OK a `false` Pokud klikne na tlačítko Storno).

![Metoda potvrdit (String) pro JavaScript zobrazuje modální objekt MessageBox na straně klienta.](adding-client-side-confirmation-when-deleting-vb/_static/image1.png)

**Obrázek 1**: metoda `confirm(string)` JavaScriptu zobrazuje modální, objekt MessageBox na straně klienta

Pokud je při odeslání formuláře vrácena hodnota `false`a z obslužné rutiny události na straně klienta, odeslání formuláře se zruší. Tato funkce umožňuje, aby obslužná rutina události Odstranit tlačítko `onclick` na straně klienta vrátila hodnotu volání `confirm("Are you sure you want to delete this product?")`. Pokud uživatel klikne na tlačítko Storno, `confirm(string)` vrátí hodnotu false, což způsobí, že odeslání formuláře bude zrušeno. Bez postbacku se neodstraní produkt, na kterém bylo tlačítko pro odstranění kliknuto. Pokud však uživatel klikne na tlačítko OK v potvrzovacím dialogovém okně, bude zpětné volání pokračovat unabated a produkt bude odstraněn. Další informace o této technice naleznete v [použití `confirm()` metody JavaScriptu k řízení odesílání formuláře](http://www.webreference.com/programming/javascript/confirm/) .

Přidání potřebného skriptu na straně klienta se mírně liší při použití šablon než při použití CommandField. Proto se v tomto kurzu podíváme na příklad FormView a GridView.

> [!NOTE]
> Pomocí technik potvrzení na straně klienta, podobně jako u těch, které jsou popsány v tomto kurzu, předpokládá, že uživatelé budou navštěvovat prohlížeče, které podporují JavaScript a mají povolený JavaScript. Pokud některé z těchto předpokladů nejsou pro konkrétního uživatele pravdivé, kliknutí na tlačítko Odstranit okamžitě způsobí postback (nezobrazuje potvrzení MessageBox).

## <a name="step-1-creating-a-formview-that-supports-deletion"></a>Krok 1: vytvoření třídy FormView podporující odstranění

Začněte přidáním třídy FormView na stránku `ConfirmationOnDelete.aspx` ve složce `EditInsertDelete` a vytvořte její vazbu na nový prvek ObjectDataSource, který vrátí zpět informace o produktu prostřednictvím metody `ProductsBLL` třídy s `GetProducts()`. Také prvek ObjectDataSource nakonfigurujte tak, aby byla metoda `ProductsBLL` třídy s `DeleteProduct(productID)` namapována na metodu ObjectDataSource s `Delete()`. Zajistěte, aby se v rozevíracích seznamech pro vložení a aktualizaci nastavily (žádné). Nakonec zaškrtněte políčko Povolit stránkování v inteligentní značce FormView s.

Po provedení tohoto postupu budou nové deklarativní označení ObjectDataSource s vypadat takto:

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample1.aspx)]

Stejně jako v předchozích příkladech, které nepoužívaly optimistickou souběžnost, je třeba vymazat vlastnost ObjectDataSource s `OldValuesParameterFormatString`.

Vzhledem k tomu, že byl svázán s ovládacím prvkem ObjectDataSource, který podporuje pouze odstranění, `ItemTemplate` FormView s nabízí pouze tlačítko Odstranit a nemá nové a aktualizovat tlačítka. Deklarativní označení FormView s obsahuje nadbytečné `EditItemTemplate` a `InsertItemTemplate`, které je možné odebrat. Věnujte prosím chvíli přizpůsobení `ItemTemplate` tak, aby se zobrazila pouze podmnožina datových polí produktu. Nakonfigurovali jsem mi, aby se název produktu zobrazil v `<h3>`ovém nadpisu nad názvem dodavatele a kategorie (společně s tlačítkem odstranit).

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample2.aspx)]

Díky těmto změnám máme plně funkční webovou stránku, která umožňuje uživateli postupně přepínat produkty, a to tak, že jednoduše kliknete na tlačítko Odstranit. Na obrázku 2 se po zobrazení v prohlížeči zobrazí snímek obrazovky s naším průběhem.

[![FormView zobrazí informace o jednom produktu.](adding-client-side-confirmation-when-deleting-vb/_static/image3.png)](adding-client-side-confirmation-when-deleting-vb/_static/image2.png)

**Obrázek 2**: třída FormView zobrazuje informace o jednom produktu ([kliknutím zobrazíte obrázek v plné velikosti).](adding-client-side-confirmation-when-deleting-vb/_static/image4.png)

## <a name="step-2-calling-the-confirmstring-function-from-the-delete-buttons-client-side-onclick-event"></a>Krok 2: volání funkce potvrdit (String) z události při kliknutí na tlačítko pro odstranění na straně klienta

Při vytvoření třídy FormView je posledním krokem konfigurace tlačítka odstranit tak, že když na něj kliká návštěvník, vyvolá se funkce JavaScript `confirm(string)`. Přidání skriptu na straně klienta k události `onclick` tlačítkem, LinkButton nebo obrázkové s na straně klienta se dá provést pomocí `OnClientClick property`, která je v ASP.NET 2,0 nová. Vzhledem k tomu, že chceme mít vrácenou hodnotu funkce `confirm(string)`, jednoduše nastavte tuto vlastnost na: `return confirm('Are you certain that you want to delete this product?');`

Po této změně by deklarativní syntaxe odstranit LinkButton s měla vypadat nějak takto:

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample3.aspx)]

To všechno je! Obrázek 3 ukazuje snímek obrazovky s tímto potvrzením v akci. Kliknutím na tlačítko Odstranit zobrazíte dialogové okno Potvrdit. Pokud uživatel klikne na zrušit, zpětné volání se zruší a produkt se neodstraní. Pokud však uživatel klikne na tlačítko OK, zpětné volání pokračuje a je vyvolána metoda ObjectDataSource s `Delete()`, ukončené záznamem v záznamu databáze.

> [!NOTE]
> Řetězec předaný do funkce `confirm(string)` JavaScriptu je oddělen apostrofy (spíše než uvozovky). V jazyce JavaScript mohou být řetězce odděleny pomocí obou znaků. Tady používáme apostrofy, aby oddělovače řetězce předaných do `confirm(string)` nevedly k nejednoznačnosti s oddělovači použitými pro hodnotu vlastnosti `OnClientClick`.

[Po kliknutí na tlačítko Odstranit se teď zobrazí ![potvrzení.](adding-client-side-confirmation-when-deleting-vb/_static/image6.png)](adding-client-side-confirmation-when-deleting-vb/_static/image5.png)

**Obrázek 3**: po kliknutí na tlačítko Odstranit se teď zobrazí potvrzení ([kliknutím zobrazíte obrázek v plné velikosti](adding-client-side-confirmation-when-deleting-vb/_static/image7.png)).

## <a name="step-3-configuring-the-onclientclick-property-for-the-delete-button-in-a-commandfield"></a>Krok 3: Konfigurace vlastnosti OnClientClick pro tlačítko Odstranit v CommandField

Při práci s tlačítkem, LinkButton nebo obrázkové přímo v šabloně můžete k ní přidružit potvrzovací dialog tak, že jednoduše nakonfigurujete jeho vlastnost `OnClientClick`, aby vracela výsledky funkce JavaScriptu `confirm(string)`. Nicméně CommandField, který přidá pole pro odstranění do prvku GridView nebo DetailsView – nemá vlastnost `OnClientClick`, která může být nastavena deklarativně. Místo toho je nutné programově odkázat na tlačítko Odstranit v prvku GridView nebo DetailsView odpovídajícím `DataBound` obslužné rutiny události a následně nastavit jeho vlastnost `OnClientClick`.

> [!NOTE]
> Při nastavení vlastnosti odstranit tlačítka `OnClientClick` v příslušné obslužné rutině události `DataBound` máme přístup k datům, které jsou svázané s aktuálním záznamem. To znamená, že můžeme zvětšit zprávu s potvrzením, aby obsahovala podrobnosti o konkrétním záznamu, například, opravdu chcete odstranit produkt Chai? " Toto přizpůsobení je možné také v šablonách pomocí syntaxe DataBinding.

Chcete-li nastavit vlastnost `OnClientClick` pro tlačítka odstranit v CommandField, přidejte na stránku prvek GridView. Proveďte konfiguraci tohoto prvku GridView pro použití stejného ovládacího prvku ObjectDataSource, který používá FormView. Také omezte BoundFields prvku GridView s tak, aby obsahovala pouze název produktu, kategorii a dodavatele. Nakonec zaškrtněte políčko Povolit odstranění z inteligentní značky GridView s. Tím se přidá CommandField do kolekce GridView `Columns` s vlastností `ShowDeleteButton` nastavenou na `true`.

Po provedení těchto změn by deklarativní označení GridView s mělo vypadat takto:

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample4.aspx)]

CommandField obsahuje jednu instanci LinkButton, ke které lze přistupovat programově z obslužné rutiny události GridView s `RowDataBound`. Po odkazování můžete vlastnost `OnClientClick` nastavit odpovídajícím způsobem. Vytvořte obslužnou rutinu události pro událost `RowDataBound` pomocí následujícího kódu:

[!code-vb[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample5.vb)]

Tato obslužná rutina události funguje s řádky dat (ty, které budou mít tlačítko Odstranit) a začínají programově odkazem na tlačítko Odstranit. V části Obecné použijte následující vzor:

[!code-vb[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample6.vb)]

*ButtonType* je typ tlačítka používaného CommandField tlačítkem, LinkButton nebo obrázkové. Ve výchozím nastavení CommandField používá LinkButtons, ale lze jej přizpůsobit prostřednictvím `ButtonType property`CommandField s. *CommandFieldIndex* je ordinální index CommandField v rámci kolekce GridView `Columns`, zatímco *controlIndex* je indexem tlačítka odstranit v rámci kolekce CommandField s `Controls`. Hodnota *controlIndex* závisí na pozici tlačítka s relativně k ostatním tlačítkům v CommandField. Pokud je například jediným tlačítkem zobrazeným v CommandField tlačítko Odstranit, použijte index 0. Pokud však existuje tlačítko pro úpravy, které předchází tlačítku odstranit, použijte index 2. Důvod, proč je použit index 2, je, protože před tlačítkem Delete jsou přidány dva ovládací prvky pomocí CommandField: tlačítko Upravit a LiteralControl, které se používají k přidání nějakého prostoru mezi tlačítky upravit a odstranit.

Pro náš konkrétní příklad má CommandField použití LinkButtons a v poli nejvíce vlevo je *commandFieldIndex* 0. Vzhledem k tomu, že nejsou k dispozici žádná další tlačítka, ale tlačítko Odstranit v CommandField, používáme *controlIndex* 0.

Po odkazování na tlačítko Odstranit v CommandField se další informace o produktu sváže s aktuálním řádkem prvku GridView. Nakonec nastavíme vlastnost tlačítka odstranit `OnClientClick` na odpovídající jazyk JavaScript, který obsahuje název produktu. Vzhledem k tomu, že řetězec jazyka JavaScript předaný do funkce `confirm(string)` je oddělený pomocí apostrofů, je nutné, aby se všechny apostrofy objevily v názvu produktu. Konkrétně všechny apostrofy v názvu produktu jsou uvozeny znakem "`\'`".

Po dokončení těchto změn se kliknutím na tlačítko Odstranit v prvku GridView zobrazí přizpůsobené potvrzovací dialogové okno (viz obrázek 4). Stejně jako u ovládacího prvku MessageBox ze třídy FormView, pokud uživatel klikne na zrušit, zpětné volání se zruší, čímž se zabrání v výskytu odstranění.

> [!NOTE]
> Tento postup lze také použít k programovému přístupu k tlačítku odstranit v CommandField v prvku DetailsView. Pro prvek DetailsView však vytvoříte obslužnou rutinu události pro událost `DataBound`, protože prvek DetailsView nemá `RowDataBound` událost.

[![kliknutím na tlačítko Odstranit GridView. se zobrazí dialogové okno přizpůsobené potvrzení.](adding-client-side-confirmation-when-deleting-vb/_static/image9.png)](adding-client-side-confirmation-when-deleting-vb/_static/image8.png)

**Obrázek 4**: kliknutím na tlačítko pro odstranění prvku GridView se zobrazí dialogové okno přizpůsobené potvrzení (Kliknutím zobrazíte[obrázek v plné velikosti).](adding-client-side-confirmation-when-deleting-vb/_static/image10.png)

## <a name="using-templatefields"></a>Použití vlastností TemplateField

Jednou z nevýhod CommandField je, že k jeho tlačítkům musí být přistup prostřednictvím indexování a výsledný objekt musí být převeden na odpovídající typ tlačítka (tlačítko, LinkButton nebo obrázkové). Použití "Magic Numbers" a pevně zakódovaných typů pozve k problémům, které nelze zjistit do doby běhu. Například pokud jste vy nebo jiný vývojář, přidá nová tlačítka do CommandField v nějakém okamžiku v budoucnosti (například tlačítko pro úpravy) nebo změní vlastnost `ButtonType`, existující kód bude stále zkompilován bez chyb, ale návštěvě stránky může způsobit výjimku nebo neočekávané chování, v závislosti na tom, jak byl kód napsán a jaké změny byly provedeny.

Alternativním řešením je převést prvky GridView a DetailsView s CommandFields na TemplateFields. Tím se vygeneruje TemplateField s `ItemTemplate`, který má LinkButton (nebo tlačítko nebo obrázkové) pro každé tlačítko v CommandField. Tato tlačítka `OnClientClick` vlastností lze přiřadit deklarativně, jak jsme viděli ve třídě FormView, nebo k nim lze programově přistupovat v příslušné obslužné rutině události `DataBound` pomocí následujícího vzoru:

[!code-vb[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample7.vb)]

Kde *controlID* je hodnota vlastnosti `ID` tlačítko s tlačítkem. I když tento model stále vyžaduje pevně zakódovaný typ pro přetypování, odstraňuje nutnost indexování, což umožňuje změnit rozložení, aniž by to vedlo k chybě za běhu.

## <a name="summary"></a>Souhrn

Funkce `confirm(string)` JavaScriptu je běžně používaná technika pro řízení pracovního postupu odeslání formuláře. Po spuštění funkce zobrazí modální dialogové okno na straně klienta, které obsahuje dvě tlačítka, OK a Storno. Pokud uživatel klikne na tlačítko OK, funkce `confirm(string)` vrátí `true`; Kliknutím na zrušit vrátíte `false`. Tato funkce, která je spojená s chováním prohlížeče s pro zrušení odeslání formuláře, pokud obslužná rutina události během procesu odeslání vrací `false`, lze použít k zobrazení potvrzovacího objektu MessageBox při odstraňování záznamu.

Funkci `confirm(string)` lze přidružit k ovládacímu prvku webového ovládacího prvku tlačítko s `onclick` obslužnou rutinu události na straně klienta prostřednictvím vlastnosti `OnClientClick` ovládacího prvku. Při práci s tlačítkem odstranit v šabloně – buď v jedné ze šablon FormView s, nebo v prvku TemplateField v ovládacím prvku DetailsView nebo GridView – Tato vlastnost může být nastavena deklarativně nebo programově, jak jsme viděli v tomto kurzu.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](implementing-optimistic-concurrency-vb.md)
> [Další](limiting-data-modification-functionality-based-on-the-user-vb.md)

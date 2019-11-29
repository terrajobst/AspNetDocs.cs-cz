---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-vb
title: Zpracování výjimek na úrovni knihoven BLL a DAL (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se dozvíte, jak tactfully zpracovávat výjimky vyvolané při aktualizaci pracovního postupu upravitelného prvku DataList.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: ca665073-b379-4239-9404-f597663ca65e
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-vb
msc.type: authoredcontent
ms.openlocfilehash: 319ab44f2e65afc77f6f89ca8aa58c529f40d05c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74624289"
---
# <a name="handling-bll--and-dal-level-exceptions-vb"></a>Zpracování výjimek na úrovni knihoven BLL a DAL (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_38_VB.exe) nebo [Stáhnout PDF](handling-bll-and-dal-level-exceptions-vb/_static/datatutorial38vb1.pdf)

> V tomto kurzu se dozvíte, jak tactfully zpracovávat výjimky vyvolané při aktualizaci pracovního postupu upravitelného prvku DataList.

## <a name="introduction"></a>Úvod

V [přehledu úprav a odstranění dat v kurzu DataList](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md) jsme vytvořili prvek DataList, který nabízí jednoduché možnosti úprav a odstranění. Přestože je plně funkční, bylo špatně uživatelsky přívětivé, protože jakákoli chyba, ke které došlo během procesu úprav nebo odstranění, způsobila neošetřenou výjimku. Pokud například vynecháte název produktu nebo, když upravujete produkt, zadáte cenovou hodnotu velmi dostupnou!, vyvolá výjimku. Vzhledem k tomu, že tato výjimka není zachycena v kódu, je podrobná až do modulu runtime ASP.NET, který pak na webové stránce zobrazí výjimky s podrobnostmi.

Jak jsme viděli při [zpracování výjimek knihoven BLL a dal v kurzu stránky ASP.NET](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) , pokud je výjimka vyvolána z hloubky obchodní logiky nebo vrstvy přístupu k datům, vrátí se podrobnosti o výjimce do prvku ObjectDataSource a následně do prvku GridView. Zjistili jsme, jak tyto výjimky řádně zpracovat vytvořením `Updated` nebo `RowUpdated` obslužných rutin událostí pro ObjectDataSource nebo GridView, kontrolou výjimky a následnou indikací, že byla výjimka zpracována.

Naše kurzy DataList ale nepoužívají prvek ObjectDataSource k aktualizaci a odstraňování dat. Místo toho pracujeme přímo na knihoven BLL. Aby bylo možné detekovat výjimky pocházející z knihoven BLL nebo DAL, musíme implementovat kód pro zpracování výjimek v rámci kódu na pozadí naší stránky ASP.NET. V tomto kurzu se dozvíte, jak více tactfully zpracovávat výjimky vyvolané během upravitelného pracovního postupu pro prvek DataList s aktualizací.

> [!NOTE]
> V tématu *Přehled úprav a odstranění dat v kurzu DataList* jsme provedli různé techniky pro úpravy a odstraňování dat z prvku DataList, některé techniky, které jsou součástí prvků ObjectDataSource pro aktualizaci a odstranění. Použijete-li tyto techniky, můžete zpracovat výjimky z knihoven BLL nebo DAL prostřednictvím obslužných rutin události ObjectDataSource `Updated` nebo `Deleted`.

## <a name="step-1-creating-an-editable-datalist"></a>Krok 1: vytvoření upravitelného prvku DataList

Předtím, než se obáváme o zpracování výjimek, ke kterým dojde během aktualizačního pracovního postupu, si nejdřív vytvořte upravitelný prvek DataList. Otevřete stránku `ErrorHandling.aspx` ve složce `EditDeleteDataList`, přidejte prvek DataList do návrháře, nastavte jeho vlastnost `ID` na `Products`a přidejte nový prvek ObjectDataSource s názvem `ProductsDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby pro výběr záznamů používal metodu `ProductsBLL` třídy s `GetProducts()`. v rozevíracích seznamech na kartách vložení, aktualizace a odstranění nastavte (žádné).

[![vrátit informace o produktu pomocí metody GetProducts ()](handling-bll-and-dal-level-exceptions-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-vb/_static/image1.png)

**Obrázek 1**: vraťte informace o produktu pomocí metody `GetProducts()` ([kliknutím zobrazíte obrázek v plné velikosti).](handling-bll-and-dal-level-exceptions-vb/_static/image3.png)

Po dokončení průvodce ObjectDataSource bude Visual Studio automaticky vytvářet `ItemTemplate` pro prvek DataList. Tuto položku nahraďte `ItemTemplate`, která zobrazuje každý název a cenu produktu a obsahuje tlačítko pro úpravy. Dále vytvořte `EditItemTemplate` s webovým ovládacím prvkem TextBox pro název a cenu a tlačítka aktualizovat a Storno. Nakonec nastavte vlastnost DataList s `RepeatColumns` na 2.

Po těchto změnách by deklarativní označení stránky mělo vypadat podobně jako následující. Dvojím zkontrolováním, že tlačítka pro úpravy, zrušení a aktualizaci mají své `CommandName` vlastnosti nastavené na upravit, zrušit a aktualizovat, v uvedeném pořadí.

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample1.aspx)]

> [!NOTE]
> Pro tento kurz musí být povolený stav zobrazení DataList s.

Počkejte, než se vám zobrazí náš průběh v prohlížeči (viz obrázek 2).

[![každý produkt zahrnuje tlačítko pro úpravy.](handling-bll-and-dal-level-exceptions-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-vb/_static/image4.png)

**Obrázek 2**: každý produkt obsahuje tlačítko pro úpravy ([kliknutím zobrazíte obrázek v plné velikosti).](handling-bll-and-dal-level-exceptions-vb/_static/image6.png)

V současné době tlačítko pro úpravy způsobuje pouze postback, který mu ještě neumožňuje upravovat produkt. Pro umožnění úprav musíme pro události `EditCommand`, `CancelCommand`a `UpdateCommand` prvku DataList vytvořit obslužné rutiny událostí. Události `EditCommand` a `CancelCommand` jednoduše aktualizují vlastnost DataList s `EditItemIndex` a znovu sváže data s DataList:

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample2.vb)]

Obslužná rutina události `UpdateCommand` je trochu větší. Musí číst v upraveném `ProductID` produktů z kolekce `DataKeys` spolu s názvem produktu a cenou z textových polí v `EditItemTemplate`, a potom před vrácením prvku DataList do jeho stavu před tím, než bude prvek DataList vracet, zavolat `UpdateProduct` metody třídy `ProductsBLL`.

Prozatím použijte pouze stejný kód z obslužné rutiny události `UpdateCommand` v *přehledu úprav a odstranění dat v kurzu DataList* . Přidáme kód pro řádný zpracování výjimek v kroku 2.

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample3.vb)]

V případě neplatného vstupu, který může mít formu nesprávně formátované jednotkové ceny, neplatnou hodnotu jednotkové ceny jako-$5,00 nebo vynechání názvu produktu, bude vyvolána výjimka. Vzhledem k tomu, že obslužná rutina události `UpdateCommand` v tomto okamžiku neobsahuje žádný kód pro zpracování výjimek, výjimka bude obsahovat až ASP.NET modul runtime, kde se zobrazí koncovému uživateli (viz obrázek 3).

![Když dojde k neošetřené výjimce, koncový uživatel uvidí chybovou stránku.](handling-bll-and-dal-level-exceptions-vb/_static/image7.png)

**Obrázek 3**: když dojde k neošetřené výjimce, koncový uživatel uvidí chybovou stránku.

## <a name="step-2-gracefully-handling-exceptions-in-the-updatecommand-event-handler"></a>Krok 2: řádné zpracování výjimek v obslužné rutině události UpdateCommand

Během pracovního postupu aktualizace mohou být výjimky v obslužné rutině události `UpdateCommand`, knihoven BLL nebo DAL. Například pokud uživatel zadá cenu, která je příliš náročná, příkaz `Decimal.Parse` v obslužné rutině události `UpdateCommand` vyvolá výjimku `FormatException`. Pokud uživatel vynechá název produktu nebo pokud má cena zápornou hodnotu, dojde k výjimce DAL.

Pokud dojde k výjimce, chceme zobrazit informativní zprávu v rámci samotné stránky. Přidejte ovládací prvek web popisku na stránku, jejíž `ID` je nastavená na `ExceptionDetails`. Nakonfigurujte text popisku, který se má zobrazit v červeném, tučném písmu a kurzívě, přiřazením jeho vlastnosti `CssClass` do `Warning` třídy šablony stylů CSS, která je definována v souboru `Styles.css`.

Když dojde k chybě, chceme, aby se popisek zobrazil jenom jednou. To znamená, že při následném postbacku by se měla zpráva s upozorněním na návěští zobrazovat. To se dá udělat tak, že buď vymažete vlastnost `Text` popisku, nebo nastavení jeho vlastnosti `Visible` na `False` v obslužné rutině události `Page_Load` (jak jsme byli zpátky v kurzu [zpracování knihoven BLL a dal výjimky na stránce ASP.NET](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) ), nebo zakázáním podpory stavu zobrazení popisku. Umožňuje použít druhou možnost.

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample4.aspx)]

Když je vyvolána výjimka, přiřadíme podrobnosti o výjimce `ExceptionDetails` vlastnosti ovládacího prvku popisek s `Text`. Vzhledem k tomu, že je stav zobrazení zakázán, při následném postbacku budou ztraceny programové změny vlastností `Text`, vrátí se zpět k výchozímu textu (prázdný řetězec), čímž se skryje zpráva upozornění.

Abychom určili, kdy došlo k chybě, aby se zobrazila užitečná zpráva na stránce, musíme do obslužné rutiny události `UpdateCommand` přidat `Try ... Catch` blok. `Try` část obsahuje kód, který může vést k výjimce, zatímco blok `Catch` obsahuje kód, který je spuštěn na tvář výjimky. Další informace o bloku `Try ... Catch` najdete v části [Základy zpracování výjimek](https://msdn.microsoft.com/library/2w8f0bss.aspx) v dokumentaci .NET Framework.

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample5.vb)]

Pokud je vyvolána výjimka jakéhokoliv typu v rámci bloku `Try`, zahájí se spuštění kódu `Catch` bloku s. Typ výjimky, která je vyvolána `DbException`, `NoNullAllowedException`, `ArgumentException`a tak dále závisí na tom, co přesně vyvolalo chybu na prvním místě. Pokud dojde k problému na úrovni databáze, bude vyvolána `DbException`. Pokud je zadána neplatná hodnota pro pole `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`nebo `ReorderLevel`, bude vyvolána `ArgumentException`, jak jsme přidali kód pro ověření těchto hodnot polí ve třídě `ProductsDataTable` (viz kurz [Vytvoření vrstvy obchodní logiky](../introduction/creating-a-business-logic-layer-vb.md) ).

Na základě textu zprávy o typu zachycené výjimky můžeme pro koncového uživatele poskytnout užitečnější vysvětlení. Následující kód, který byl použit v téměř totožném tvaru zpět při [zpracování výjimek knihoven BLL a dal v kurzu stránky ASP.NET](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) , poskytuje tuto úroveň podrobností:

[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample6.vb)]

Chcete-li dokončit tento kurz, jednoduše zavolejte metodu `DisplayExceptionDetails` z bloku `Catch`, který je předaný v zachycené instanci `Exception` (`ex`).

U `Try ... Catch`ho blokování se uživatelům zobrazí více informativní chybová zpráva, jak je znázorněno na obrázcích 4 a 5. Všimněte si, že v tváři výjimky zůstane prvek DataList v režimu úprav. Důvodem je, že jakmile dojde k výjimce, tok řízení je okamžitě přesměrován na blok `Catch` a obejít kód, který prvek DataList vrátí do svého stavu před úpravou.

[![se zobrazí chybová zpráva, pokud uživatel vynechá požadované pole](handling-bll-and-dal-level-exceptions-vb/_static/image9.png)](handling-bll-and-dal-level-exceptions-vb/_static/image8.png)

**Obrázek 4**: Pokud uživatel vynechá požadované pole ([kliknutím zobrazíte obrázek v plné velikosti](handling-bll-and-dal-level-exceptions-vb/_static/image10.png)), zobrazí se chybová zpráva.

[Při zadání záporné ceny ![zobrazit chybovou zprávu](handling-bll-and-dal-level-exceptions-vb/_static/image12.png)](handling-bll-and-dal-level-exceptions-vb/_static/image11.png)

**Obrázek 5**: při zadání záporné ceny se zobrazí chybová zpráva ([kliknutím zobrazíte obrázek v plné velikosti](handling-bll-and-dal-level-exceptions-vb/_static/image13.png)).

## <a name="summary"></a>Přehled

GridView a ObjectDataSource poskytují obslužné rutiny události na úrovni, které obsahují informace o všech výjimkách, které byly vyvolány během procesu aktualizace a odstranění, a také vlastnosti, které lze nastavit tak, aby označovaly, zda byla výjimka zpracována. Tyto funkce jsou však nedostupné při práci s DataList a přímé použití knihoven BLL. Místo toho zodpovídáme za implementaci zpracování výjimek.

V tomto kurzu jsme viděli, jak přidat zpracování výjimek do upravitelného pracovního postupu DataList s, přidáváním `Try ... Catch` bloku do obslužné rutiny události `UpdateCommand`. Pokud je vyvolána výjimka během pracovního postupu aktualizace, spustí se kód `Catch` bloku s a zobrazí se užitečné informace v popisku `ExceptionDetails`.

V tomto okamžiku DataList neprovede žádné úsilí, aby nedocházelo k výjimkám na prvním místě. I když ví, že záporná cena bude mít za následek výjimku, zatím jsme nepřidali žádné funkce pro proaktivní zabránění uživatelům v zadávání takového neplatného vstupu. V našem dalším kurzu se dozvíte, jak přispět k omezení výjimek způsobených neplatným uživatelským vstupem přidáním ovládacích prvků ověřování v `EditItemTemplate`.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Pokyny k návrhu pro výjimky](https://msdn.microsoft.com/library/ms298399.aspx)
- [Protokolování chyb modulů a obslužných rutin (knihovny elmah)](http://workspaces.gotdotnet.com/elmah) (Open source knihovna pro chyby protokolování)
- [Podniková knihovna pro .NET Framework 2,0](https://www.microsoft.com/downloads/details.aspx?familyid=5A14E870-406B-4F2A-B723-97BA84AE80B5&amp;displaylang=en) (zahrnuje blok aplikace pro správu výjimek)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Ken Pespisa. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](performing-batch-updates-vb.md)
> [Další](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)

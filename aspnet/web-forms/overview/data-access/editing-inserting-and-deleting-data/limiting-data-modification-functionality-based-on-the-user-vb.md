---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb
title: Omezení funkcí pro úpravu dat podle uživatele (VB) | Microsoft Docs
author: rick-anderson
description: Ve webové aplikaci, která umožňuje uživatelům upravovat data, mohou mít různé uživatelské účty různá oprávnění k úpravám dat. V tomto kurzu podíváme se, jak t...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 9dc264a6-feb8-474b-8b91-008c50708065
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb
msc.type: authoredcontent
ms.openlocfilehash: c257a930e4d27fcd42591a541e700786bf413bf0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74627183"
---
# <a name="limiting-data-modification-functionality-based-on-the-user-vb"></a>Omezení funkcí pro úpravu dat podle uživatele (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_23_VB.exe) nebo [Stáhnout PDF](limiting-data-modification-functionality-based-on-the-user-vb/_static/datatutorial23vb1.pdf)

> Ve webové aplikaci, která umožňuje uživatelům upravovat data, mohou mít různé uživatelské účty různá oprávnění k úpravám dat. V tomto kurzu podíváme se, jak dynamicky upravovat možnosti změny dat na základě navštíveného uživatele.

## <a name="introduction"></a>Úvod

Řada webových aplikací podporuje uživatelské účty a poskytuje různé možnosti, sestavy a funkce na základě přihlášeného uživatele. V našich kurzech bychom například chtěli dovolit, aby se uživatelé od dodavatelů přihlásili k webu a aktualizovali Obecné informace o svých produktech – jejich jméno a množství na jednotku, případně i informace o dodavatelích, jako je název společnosti. Adresa: informace o kontaktní osobě a tak dále. Kromě toho můžeme chtít zahrnout některé uživatelské účty pro lidi z naší společnosti, aby se mohli přihlásit a aktualizovat informace o produktech jako jednotky na skladě, změnit pořadí a tak dále. Naše webová aplikace může také uživatelům umožnit, aby navštívili (uživatelé, kteří ještě nejsou přihlášení), ale omezili si jejich zobrazení jenom na data. V rámci tohoto systému uživatelských účtů chceme, aby webové ovládací prvky dat na našich ASP.NET stránkách nabízely možnosti vkládání, úprav a odstraňování, které jsou vhodné pro aktuálně přihlášeného uživatele.

V tomto kurzu podíváme se, jak dynamicky upravovat možnosti změny dat na základě navštíveného uživatele. Konkrétně vytvoříme stránku, která zobrazí informace o dodavatelích v upravitelném ovládacím prvku DetailsView spolu s prvku GridView, který obsahuje seznam produktů poskytovaných dodavatelem. Pokud uživatel navštívil stránku z naší společnosti, může: zobrazit informace o dodavatelích; upravit jejich adresu; a upravte informace pro jakýkoli produkt poskytovaný dodavatelem. Pokud je však uživatel z konkrétní společnosti, může zobrazit a upravit pouze vlastní informace o adrese a upravovat pouze své produkty, které nebyly označeny jako ukončené.

[![může uživatel z naší společnosti upravovat informace o dodavatelích.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image2.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image1.png)

**Obrázek 1**: uživatel z naší společnosti může upravovat informace o dodavatelích ([kliknutím zobrazíte obrázek v plné velikosti).](limiting-data-modification-functionality-based-on-the-user-vb/_static/image3.png)

[![uživatel z konkrétního dodavatele může zobrazit a upravit pouze své informace](limiting-data-modification-functionality-based-on-the-user-vb/_static/image5.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image4.png)

**Obrázek 2**: uživatel z konkrétního dodavatele může zobrazit a upravit pouze své informace ([kliknutím zobrazíte obrázek v plné velikosti](limiting-data-modification-functionality-based-on-the-user-vb/_static/image6.png)).

Pojďme začít!

> [!NOTE]
> Systém členství v ASP.NET 2,0 s poskytuje standardizovanou a rozšiřitelnou platformu pro vytváření, správu a ověřování uživatelských účtů. Vzhledem k tomu, že přezkoumání systému členství je nad rámec těchto kurzů, tento kurz místo toho "předstírá" členství, protože umožňuje anonymním návštěvníkům zvolit, zda jsou od konkrétního dodavatele nebo z naší společnosti. Další informace o členství najdete v článku věnovaném [kontrole členství, rolí a datových řad v ASP.NET 2,0 s](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx) .

## <a name="step-1-allowing-the-user-to-specify-their-access-rights"></a>Krok 1: umožnění uživateli zadat přístupová práva

V reálné webové aplikaci obsahují informace o účtu uživatele informace o tom, zda pracovaly pro naši společnost nebo konkrétního dodavatele, a tyto informace budou programově přístupné z našich stránek ASP.NET po přihlášení uživatele k webu. Tyto informace mohou být zachyceny prostřednictvím systému rolí ASP.NET 2,0 s, jako informace o účtu na úrovni uživatele přes profilový systém nebo prostřednictvím některých vlastních prostředků.

Vzhledem k tomu, že cílem tohoto kurzu je předvedení úprav možností změny dat na základě přihlášeného uživatele a není určeno k tomu, aby procházela členství, role a systémy profilů ASP.NET 2,0 s, využijeme jednoduše mechanizmus pro určení možnosti pro uživatele, kteří navštívili stránku – DropDownList, ze kterého může uživatel určit, jestli mají být schopni zobrazit a upravit jakékoli informace o dodavatelích nebo případně také informace o dodavateli, které mohou zobrazit a upravit. Pokud uživatel informuje o tom, že může zobrazit a upravit informace o dodavateli (výchozí), může stránku procházet všemi dodavateli, upravovat informace o dodavatelích a upravovat název a množství jednotek pro všechny produkty poskytované vybraným dodavatelem. Pokud uživatel informuje, že může pouze zobrazit a upravit konkrétního dodavatele, může zobrazit pouze podrobnosti a produkty pro tohoto dodavatele a může aktualizovat pouze název a množství informací o jednotce pro tyto produkty, *které nejsou* ukončeny.

Náš první krok v tomto kurzu, pak je vytvořit tuto DropDownList a naplnit ji dodavateli v systému. Otevřete stránku `UserLevelAccess.aspx` ve složce `EditInsertDelete`, přidejte DropDownList, jehož vlastnost `ID` je nastavena na `Suppliers`a navažte tuto vlastnost DropDownList na nový prvek ObjectDataSource s názvem `AllSuppliersDataSource`.

[![vytvořit nový prvek ObjectDataSource s názvem AllSuppliersDataSource](limiting-data-modification-functionality-based-on-the-user-vb/_static/image8.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image7.png)

**Obrázek 3**: vytvoření nového prvku ObjectDataSource s názvem `AllSuppliersDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](limiting-data-modification-functionality-based-on-the-user-vb/_static/image9.png))

Vzhledem k tomu, že chceme, aby tato třída DropDownList zahrnovala všechny dodavatele, nakonfigurujte prvek ObjectDataSource, aby vyvolala metodu `SuppliersBLL` třídy s `GetSuppliers()`. Také zajistěte, aby byla metoda ObjectDataSource s `Update()` namapována na metodu `SuppliersBLL` třídy s `UpdateSupplierAddress`, protože tento prvek ObjectDataSource bude také použit ovládacím prvkem DetailsView, který budeme přidávat v kroku 2.

Po dokončení průvodce ObjectDataSource dokončete postup konfigurací `Suppliers` DropDownList tak, aby se zobrazilo `CompanyName` datové pole a jako hodnotu pro každý `ListItem`používá pole `SupplierID` data.

[![konfigurace DropDownList pro dodavatele pro použití datových polí CompanyName a KódDodavatele](limiting-data-modification-functionality-based-on-the-user-vb/_static/image11.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image10.png)

**Obrázek 4**: Konfigurace `Suppliers` DropDownList pro použití datových polí `CompanyName` a `SupplierID` ([kliknutím zobrazíte obrázek v plné velikosti](limiting-data-modification-functionality-based-on-the-user-vb/_static/image12.png))

V tomto okamžiku zobrazí DropDownList názvy společností dodavatelů v databázi. Je ale také potřeba do DropDownList přidat možnost Zobrazit/upravit všechny dodavatele. Pokud to chcete provést, nastavte vlastnost `Suppliers` DropDownList s `AppendDataBoundItems` na `true` a pak přidejte `ListItem`, jehož vlastnost `Text` je "Zobrazit/upravit všechny dodavatele" a jehož hodnota je `-1`. To lze přidat přímo prostřednictvím deklarativní značky nebo pomocí návrháře tak, že přejdete na okno Vlastnosti a kliknete na tři tečky ve vlastnosti DropDownList s `Items`.

> [!NOTE]
> Pokud chcete podrobnější diskuzi o přidání položky Select All do ovládacího prvkem DropDownList vázaného na data, přečtěte si téma [*filtrování hlavní/podrobnosti pomocí kurzu DropDownList*](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) .

Po nastavení vlastnosti `AppendDataBoundItems` a přidání `ListItem` by deklarativní označení DropDownList mělo vypadat takto:

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample1.aspx)]

Obrázek 5 ukazuje snímek obrazovky s aktuálním průběhem při prohlížení v prohlížeči.

[![ec DropDownList pro dodavatele obsahuje hodnotu Zobrazit vše v seznamu a jednu pro každého dodavatele.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image14.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image13.png)

**Obrázek 5**: `Suppliers` DropDownList obsahuje příkaz Show All `ListItem`a jeden pro každého dodavatele ([kliknutím zobrazíte obrázek v plné velikosti).](limiting-data-modification-functionality-based-on-the-user-vb/_static/image15.png)

Vzhledem k tomu, že chceme aktualizovat uživatelské rozhraní hned po změně výběru uživatelem, nastavte vlastnost `Suppliers` DropDownList s `AutoPostBack` na `true`. V kroku 2 vytvoříme ovládací prvek DetailsView, který zobrazí informace o dodavatelích na základě výběru DropDownList. V kroku 3 potom vytvoříme obslužnou rutinu události pro tuto událost DropDownList s `SelectedIndexChanged`, do které přidáte kód, který sváže příslušné informace o dodavateli s ovládacím prvkem na základě vybraného dodavatele.

## <a name="step-2-adding-a-detailsview-control"></a>Krok 2: Přidání ovládacího prvku DetailsView

Umožňuje použít prvek DetailsView k zobrazení informací o dodavateli. Pro uživatele, který může zobrazit a upravit všechny dodavatele, bude ovládací prvek DetailsView podporovat stránkování, což uživateli umožňuje procházet informace o dodavateli v jednom okamžiku. Pokud je však uživatel pro konkrétního dodavatele fungovat, zobrazí se v ovládacím prvku DetailsView pouze konkrétní informace o dodavatelích a nebude zahrnovat rozhraní stránkování. V obou případech musí DetailsView uživateli dovolit, aby upravil pole Adresa dodavatele, města a země.

Přidejte prvek DetailsView na stránku pod `Suppliers` DropDownList, nastavte jeho vlastnost `ID` na `SupplierDetails`a navažte ji na `AllSuppliersDataSource` ObjectDataSource vytvořeném v předchozím kroku. Potom zaškrtněte políčka Povolit stránkování a povolit úpravy z inteligentní značky DetailsView s.

> [!NOTE]
> Pokud nevidíte možnost Povolit úpravy v inteligentní značce DetailsView s, protože jste nemapovali metodu ObjectDataSource s `Update()` na metodu `SuppliersBLL` třídy s `UpdateSupplierAddress`. Chvíli počkejte, než se vrátíte zpátky a udělejte tuto změnu konfigurace, po které by se měla možnost Povolit úpravy zobrazit v inteligentní značce DetailsView s.

Vzhledem k tomu, že metoda `SuppliersBLL` třídy s `UpdateSupplierAddress` přijímá pouze čtyři parametry-`supplierID`, `address`, `city`a `country`-upravit ovládací prvek DetailsView s BoundFields tak, aby `CompanyName` a `Phone` BoundFields jsou jen pro čtení. Kromě toho odeberte `SupplierID` vlastnost BoundField zcela. Nakonec má `AllSuppliersDataSource` ObjectDataSource aktuálně má svou vlastnost `OldValuesParameterFormatString` nastavenou na `original_{0}`. Chvíli odeberte nastavení této vlastnosti z deklarativní syntaxe nebo ji nastavte na výchozí hodnotu, `{0}`.

Po nakonfigurování `SupplierDetails` DetailsView a `AllSuppliersDataSource` ObjectDataSource budeme mít následující deklarativní označení:

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample2.aspx)]

V tomto okamžiku může být element DetailsView stránkou a zvolené informace o adrese dodavatele lze aktualizovat bez ohledu na výběr, který jste provedli v `Suppliers` DropDownList (viz obrázek 6).

[![se můžou zobrazit informace o dodavatelích a její adresa se aktualizuje.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image17.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image16.png)

**Obrázek 6**: informace o všech dodavatelích se dají zobrazit a její adresa se aktualizovala ([kliknutím zobrazíte obrázek v plné velikosti).](limiting-data-modification-functionality-based-on-the-user-vb/_static/image18.png)

## <a name="step-3-displaying-only-the-selected-supplier-s-information"></a>Krok 3: zobrazení pouze vybraných informací o dodavateli

Na naší stránce jsou aktuálně zobrazeny informace pro všechny dodavatele bez ohledu na to, zda byl vybrán konkrétní dodavatel z `Suppliers` DropDownList. Aby bylo možné zobrazit jenom informace o dodavatelích pro vybraného dodavatele, musíme na naši stránku přidat další prvek ObjectDataSource, což načte informace o určitém dodavateli.

Přidejte na stránku nový prvek ObjectDataSource a pojmenujte ho `SingleSupplierDataSource`. Z inteligentní značky klikněte na odkaz Konfigurovat zdroj dat a použijte metodu `GetSupplierBySupplierID(supplierID)` `SuppliersBLL` třídy s. Stejně jako u `AllSuppliersDataSource` ObjectDataSource mají `SingleSupplierDataSource` prvek ObjectDataSource s `Update()` namapovaný na `UpdateSupplierAddress` metodu `SuppliersBLL` třídy s.

[![nakonfigurovat prvek ObjectDataSource SingleSupplierDataSource na použití metody GetSupplierBySupplierID (KódDodavatele)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image20.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image19.png)

**Obrázek 7**: Konfigurace `SingleSupplierDataSource` ObjectDataSource pro použití metody `GetSupplierBySupplierID(supplierID)` ([kliknutím zobrazíte obrázek v plné velikosti](limiting-data-modification-functionality-based-on-the-user-vb/_static/image21.png))

V dalším kroku se zobrazí výzva k zadání zdroje parametrů pro `GetSupplierBySupplierID(supplierID)` metoda s `supplierID` vstupním parametrem. Vzhledem k tomu, že chceme zobrazit informace pro dodavatele vybrané z DropDownList, použijte jako zdroj parametru vlastnost `Suppliers` DropDownList s `SelectedValue`.

[![jako zdroj parametru ČísloDodavatele použít DropDownList pro dodavatele](limiting-data-modification-functionality-based-on-the-user-vb/_static/image23.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image22.png)

**Obrázek 8**: jako zdroj parametru `supplierID` použijte `Suppliers` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti).](limiting-data-modification-functionality-based-on-the-user-vb/_static/image24.png)

I s tímto druhým prvkem ObjectDataSource přidány je ovládací prvek DetailsView aktuálně nakonfigurován tak, aby vždy používal `AllSuppliersDataSource` ObjectDataSource. Musíme přidat logiku pro úpravu zdroje dat používaného ovládacím prvkem DetailsView v závislosti na vybrané položce `Suppliers` DropDownList. K tomuto účelu vytvořte obslužnou rutinu události `SelectedIndexChanged` pro DropDownList pro dodavatele. To lze snadno vytvořit dvojitým kliknutím na DropDownList v návrháři. Tato obslužná rutina události musí určit, jaký zdroj dat se má použít, a musí znovu vytvořit vazby dat k prvku DetailsView. Toho je možné dosáhnout pomocí následujícího kódu:

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample3.vb)]

Obslužná rutina události začíná tím, že určí, zda byla vybrána možnost Zobrazit/upravit všechny dodavatele. Pokud byl, nastaví `SupplierDetails` DetailsView s `DataSourceID` na `AllSuppliersDataSource` a vrátí uživatele k prvnímu záznamu v sadě dodavatelů nastavením vlastnosti `PageIndex` na hodnotu 0. Pokud však uživatel vybral konkrétního dodavatele z DropDownList, `DataSourceID` ovládacího prvku DetailsView přiřazen `SingleSuppliersDataSource`. Bez ohledu na to, jaký zdroj dat se používá, je režim `SuppliersDetails` vrácen zpět do režimu jen pro čtení a data jsou znovu svázána s ovládacím prvkem DetailsView voláním metody `SuppliersDetails` Control s `DataBind()`.

V rámci této obslužné rutiny události nyní ovládací prvek DetailsView zobrazuje vybraného dodavatele, pokud nebyla vybrána možnost Zobrazit/upravit všechny dodavatele. v takovém případě lze všechny dodavatele zobrazit přes rozhraní stránkování. Obrázek 9 zobrazí stránku s vybranou možností zobrazit/upravit všechny dodavatele; Všimněte si, že rozhraní stránkování je k dispozici a umožňuje uživateli navštívit a aktualizovat libovolného dodavatele. Obrázek 10 ukazuje stránku s vybraným dodavatelem Ma Maison. V tomto případě se v tomto případě v tomto případě dá zobrazit a upravit jenom informace Ma Maison.

[![se všechny informace o dodavatelích dají zobrazit a upravit.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image26.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image25.png)

**Obrázek 9**: můžete zobrazit a upravit všechny informace o dodavatelích ([kliknutím zobrazíte obrázek v plné velikosti).](limiting-data-modification-functionality-based-on-the-user-vb/_static/image27.png)

[![zobrazit a upravit lze pouze vybrané informace dodavatele.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image29.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image28.png)

**Obrázek 10**: zobrazit a upravit lze pouze vybrané informace dodavatele ([kliknutím zobrazíte obrázek v plné velikosti).](limiting-data-modification-functionality-based-on-the-user-vb/_static/image30.png)

> [!NOTE]
> Pro tento kurz musí být ovládací prvek DropDownList i DetailsView `EnableViewState` nastavena na `true` (výchozí), protože změny vlastností ovládacího prvku DropDownList s `SelectedIndex` a ovládacího prvku DetailsView s `DataSourceID` musí být zapamatovatelné napříč zpětnými voláními.

## <a name="step-4-listing-the-suppliers-products-in-an-editable-gridview"></a>Krok 4: výpis produktů dodavatelů do upravitelného prvku GridView

Po dokončení našeho prvku DetailsView je dalším krokem zahrnutí upravitelného prvku GridView, který obsahuje seznam produktů poskytovaných vybraným dodavatelem. Tento prvek GridView by měl umožňovat úpravy pouze polí `ProductName` a `QuantityPerUnit`. Pokud uživatel, který stránku navštíví, pochází z konkrétního dodavatele, mělo by to umožňovat pouze aktualizace těchto produktů, *které nejsou* ukončeny. Abychom to mohli udělat, musíte nejdřív přidat přetížení metody `ProductsBLL` třídy s `UpdateProducts`, která přebírá pouze pole `ProductID`, `ProductName`a `QuantityPerUnit` jako vstupy. V mnoha kurzech jsme tento proces předem provedli, takže Podívejme se jenom na kód, který by měl být přidaný do `ProductsBLL`:

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample4.vb)]

Po vytvoření tohoto přetížení se znovu připravujeme k přidání ovládacího prvku GridView a jeho přidruženého prvku ObjectDataSource. Přidejte na stránku nový prvek GridView, nastavte jeho vlastnost `ID` na `ProductsBySupplier`a nakonfigurujte ji tak, aby používala nový prvek ObjectDataSource s názvem `ProductsBySupplierDataSource`. Vzhledem k tomu, že chceme, aby tento prvek GridView vypisovat tyto produkty vybraným dodavatelem, použijte metodu `GetProductsBySupplierID(supplierID)` `ProductsBLL` třídy s. Namapujte také metodu `Update()` na nové přetížení `UpdateProduct`, které jsme právě vytvořili.

[![nakonfigurovat prvek ObjectDataSource na použití právě vytvořeného přetížení UpdateProduct](limiting-data-modification-functionality-based-on-the-user-vb/_static/image32.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image31.png)

**Obrázek 11**: Konfigurace prvku ObjectDataSource pro použití právě vytvořeného přetížení `UpdateProduct` ([kliknutím zobrazíte obrázek v plné velikosti](limiting-data-modification-functionality-based-on-the-user-vb/_static/image33.png))

Po zobrazení výzvy k výběru zdroje parametrů pro `supplierID` vstupní parametr `GetProductsBySupplierID(supplierID)` metoda. Vzhledem k tomu, že chceme Zobrazit produkty pro dodavatele vybrané v ovládacím prvku DetailsView, použijte jako zdroj parametru vlastnost `SuppliersDetails` DetailsView Control s `SelectedValue`.

[![jako zdroj parametru použít vlastnost SuppliersDetails DetailsView s SelectedValue](limiting-data-modification-functionality-based-on-the-user-vb/_static/image35.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image34.png)

**Obrázek 12**: použití vlastnosti `SuppliersDetails` DetailsView s `SelectedValue` jako zdroje parametru ([kliknutím zobrazíte obrázek v plné velikosti](limiting-data-modification-functionality-based-on-the-user-vb/_static/image36.png))

Pokud se vrátíte do prvku GridView, odeberte všechna pole GridView s výjimkou `ProductName`, `QuantityPerUnit`a `Discontinued`a označte `Discontinued` třídě CheckBoxField podporována jako jen pro čtení. Také zaškrtněte možnost Povolit úpravy z inteligentní značky GridView s. Po provedení těchto změn by deklarativní označení ovládacího prvku GridView a ObjectDataSource mělo vypadat podobně jako následující:

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample5.aspx)]

Stejně jako u našich předchozích ObjectDataSource je tato vlastnost `OldValuesParameterFormatString` nastavena na hodnotu `original_{0}`, což způsobí problémy při pokusu o aktualizaci názvu produktu nebo množství na jednotku. Odeberte tuto vlastnost z deklarativní syntaxe úplně nebo ji nastavte na výchozí `{0}`.

Po dokončení této konfigurace na naší stránce se teď zobrazí seznam produktů poskytovaných dodavatelem vybraným v prvku GridView (viz obrázek 13). V současné době je možné aktualizovat *libovolný* název produktu nebo množství na jednotku. Musíme ale aktualizovat naši logiku stránky tak, aby byly tyto funkce pro uživatele přidružené k určitému dodavateli zakázané pro ukončené produkty. Tento závěrečný kámen provedeme v kroku 5.

[Zobrazí se ![produktů poskytovaných vybraným dodavatelem.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image38.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image37.png)

**Obrázek 13**: zobrazí se produkty poskytované vybraným dodavatelem ([kliknutím zobrazíte obrázek v plné velikosti](limiting-data-modification-functionality-based-on-the-user-vb/_static/image39.png)).

> [!NOTE]
> Přidáním tohoto upravitelného prvku GridView by se měla aktualizovat obslužná rutina události `Suppliers` DropDownList s `SelectedIndexChanged`, aby vracela prvek GridView do stavu jen pro čtení. V opačném případě je v případě, že je v úpravě informací o produktu vybrán jiný dodavatel, odpovídající index v prvku GridView pro nového dodavatele bude také možné upravovat. Chcete-li tomu zabránit, jednoduše nastavte vlastnost GridView s `EditIndex` na `-1` v obslužné rutině události `SelectedIndexChanged`.

Také si vyvoláte, že je důležité, aby byl povolen stav zobrazení GridView s (výchozí chování). Pokud nastavíte vlastnost `EnableViewState` prvku GridView s na hodnotu `false`, spustíte riziko, že neúmyslně odstraní nebo upraví záznamy v souběžných uživatelích. Viz [Upozornění: problém souběžnosti s ASP.NET 2,0 gridviews/DetailsView/formviews, které podporují úpravy a/nebo odstraňování a jejichž stav zobrazení je zakázán](http://scottonwriting.net/sowblog/posts/10054.aspx) pro další informace.

## <a name="step-5-disallow-editing-for-discontinued-products-when-showedit-all-suppliers-is-not-selected"></a>Krok 5: Zákaz úprav pro ukončené produkty, když není vybraná možnost Zobrazit/upravit všechny dodavatele

I když je prvek GridView `ProductsBySupplier` plně funkční, aktuálně uděluje uživatelům, kteří jsou od konkrétního dodavatele, příliš velký přístup. Podle našich obchodních pravidel by tito uživatelé neměli moct aktualizovat vyřazené produkty. K vykonání tohoto problému můžeme skrýt (nebo zakázat) tlačítko Upravit v těchto řádcích GridView s ukončenými produkty, pokud je stránka navštívená uživatelem od dodavatele.

Vytvořte obslužnou rutinu události pro `RowDataBound` událost GridView. V této obslužné rutině je potřeba určit, jestli je uživatel přidružený ke konkrétnímu dodavateli, který je pro tento kurz určený, a to tak, že zkontroluje `SelectedValue` vlastnost dodavatelé pro dodavatele – Pokud je to něco jiného než-1, bude uživatel přidružený k určitému dodavateli. Pro tyto uživatele je pak potřeba určit, jestli je produkt vyřazený. Odkaz na skutečnou instanci `ProductRow` spojenou s řádkem GridView lze vytvořit prostřednictvím vlastnosti `e.Row.DataItem`, jak je popsáno v kurzu [*zobrazení souhrnných informací v tomto kurzu pro prvky GridView*](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) . Pokud je produkt vyřazený, můžeme pomocí technik popsaných v předchozím kurzu přikázat na tlačítko pro úpravy v prvku GridView s CommandField a [*Přidat potvrzení na straně klienta*](adding-client-side-confirmation-when-deleting-vb.md). Až budeme mít odkaz, můžeme tlačítko skrýt nebo zakázat.

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample6.vb)]

Pokud je tato obslužná rutina události na místě, když navštívíte tuto stránku jako uživatel od konkrétního dodavatele, tyto produkty, které jsou vyřazené, nejsou editovatelné, protože pro tyto produkty je tlačítko Upravit skryté. Například "Anton" s Gumbo mix je Nepokračující produkt pro nového dodavatele Orleans Cajun. Při návštěvě stránky pro tohoto konkrétního dodavatele je tlačítko Upravit pro tento produkt skryté od pohledu (viz obrázek 14). Když ale navštívíte pomocí možnosti Zobrazit/upravit všechny dodavatele, zpřístupní se tlačítko Upravit (viz obrázek 15).

[![pro uživatele, kteří jsou konkrétní pro dodavatele, je tlačítko Upravit pro Gumbo pro Anton s](limiting-data-modification-functionality-based-on-the-user-vb/_static/image41.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image40.png)

**Obrázek 14**: u uživatelů specifických pro dodavatele je tlačítko Upravit pro Anton, které je Gumbo, skryté ([kliknutím zobrazíte obrázek v plné velikosti).](limiting-data-modification-functionality-based-on-the-user-vb/_static/image42.png)

[![pro zobrazit nebo upravit všechny uživatele dodavatelů se zobrazí tlačítko Upravit pro Anton s Gumboem.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image44.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image43.png)

**Obrázek 15**: u Zobrazit/upravit všechny uživatele dodavatelů se zobrazí tlačítko Upravit pro Anton, která obsahuje Gumbo ([kliknutím zobrazíte obrázek v plné velikosti).](limiting-data-modification-functionality-based-on-the-user-vb/_static/image45.png)

## <a name="checking-for-access-rights-in-the-business-logic-layer"></a>Kontrola přístupových práv ve vrstvě obchodní logiky

V tomto kurzu stránka ASP.NET zpracovává veškerou logiku s ohledem na informace, které uživatel uvidí a jaké produkty může aktualizovat. V ideálním případě by tato logika byla také přítomna ve vrstvě obchodní logiky. Například metoda `SuppliersBLL` třídy s `GetSuppliers()` (která vrací všechny dodavatele) může obsahovat kontrolu, aby se zajistilo, že aktuálně přihlášený uživatel *není* přidružen ke konkrétnímu dodavateli. Podobně `UpdateSupplierAddress` metoda by mohla zahrnovat kontrolu, aby se zajistilo, že aktuálně přihlášený uživatel pracoval pro naši společnost (a proto může aktualizovat všechny informace o adrese dodavatele) nebo je přidružený k dodavateli, jehož data se aktualizují.

Nezahrnuli jsme sem tyto knihoven BLL kontroly, protože v našem kurzu jsou práva uživatele určena pomocí ovládacího prvkem DropDownList na stránce, ke kterému třídy knihoven BLL získat přístup. Při používání systému členství nebo jednoho z předem připravených ověřovacích schémat poskytovaných službou ASP.NET (například ověřování systému Windows) je přístup k informacím a rolím aktuálně přihlášeného uživatele z knihoven BLL, čímž se takový přístup stane. Kontrola práv je možná na prezentační i knihoven BLL vrstvě.

## <a name="summary"></a>Přehled

Většina webů, které poskytují uživatelské účty, musí přizpůsobit rozhraní změny dat na základě přihlášeného uživatele. Uživatelé s právy pro správu mohou odstranit a upravit jakýkoli záznam, zatímco uživatelé bez oprávnění správce mohou být omezeni pouze na aktualizaci nebo odstranění záznamů, které sami vytvořili. Bez ohledu na to, jak scénář může být, lze rozšířit třídy dat webové ovládací prvky, prvky ObjectDataSource a obchodní logiky tak, aby na základě přihlášeného uživatele mohli přidat nebo zamítnout určité funkce. V tomto kurzu jsme viděli, jak omezit zobrazitelná a upravitelná data v závislosti na tom, jestli byl uživatel přidružený ke konkrétnímu dodavateli nebo jestli pracoval pro naši společnost.

V tomto kurzu se uzavírá naše zkoumání vkládání, aktualizace a odstraňování dat pomocí ovládacích prvků GridView, DetailsView a FormView. Počínaje dalším kurzem vám budeme věnovat pozornost přidání podpory stránkování a řazení.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](adding-client-side-confirmation-when-deleting-vb.md)

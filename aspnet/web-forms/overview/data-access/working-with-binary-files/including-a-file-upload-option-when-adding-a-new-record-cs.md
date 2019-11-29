---
uid: web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
title: Zahrnutí možnosti nahrání souboru při přidání nového záznamu (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se dozvíte, jak vytvořit webové rozhraní, které umožňuje uživateli zadat textová data a nahrát binární soubory. K ilustraci dostupných možností t...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 362ade25-3965-4fb2-88d2-835c4786244f
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
msc.type: authoredcontent
ms.openlocfilehash: f1287e180151b3034a7b90ef4b3f1fbe68354a09
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74577169"
---
# <a name="including-a-file-upload-option-when-adding-a-new-record-c"></a>Zahrnutí možnosti nahrání souboru při přidání nového záznamu (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_56_CS.exe) nebo [Stáhnout PDF](including-a-file-upload-option-when-adding-a-new-record-cs/_static/datatutorial56cs1.pdf)

> V tomto kurzu se dozvíte, jak vytvořit webové rozhraní, které umožňuje uživateli zadat textová data a nahrát binární soubory. K ilustraci možností dostupných pro ukládání binárních dat se v databázi uloží jeden soubor, zatímco druhý je uložený v systému souborů.

## <a name="introduction"></a>Úvod

V předchozích dvou kurzech jsme prozkoumali techniky pro ukládání binárních dat, která jsou přidružená k datovému modelu aplikace s. prohlédli jsme si, jak pomocí ovládacího prvku pro nahrání souborů odesílat soubory z klienta na webový server a jak prezentovat tato binární data v datech. ovládací prvek eb Ještě máme mluvit o tom, jak přidružit nahraná data k datovému modelu, ale.

V tomto kurzu vytvoříme webovou stránku, na které se přidá nová kategorie. Kromě textových polí pro název a Popis kategorie a bude tato stránka muset zahrnovat dva ovládací prvky pro nahrání souborů pro nový obrázek kategorie a jeden pro brožuru. Nahraný obrázek bude uložen přímo ve sloupci nový záznam s `Picture`, zatímco brožura bude uložena do složky `~/Brochures` s cestou k souboru uloženému ve sloupci nový záznam s `BrochurePath`.

Před vytvořením této nové webové stránky budeme muset architekturu aktualizovat. Hlavní dotaz `CategoriesTableAdapter` s nenačítá `Picture` sloupci. V důsledku toho metoda automaticky generovaného `Insert` má pouze vstupy pro pole `CategoryName`, `Description`a `BrochurePath`. Proto musíme v TableAdapter vytvořit další metodu, která vyzve k zadání všech čtyř `Categories` polí. Třída `CategoriesBLL` v vrstvě obchodní logiky bude také muset aktualizovat.

## <a name="step-1-adding-aninsertwithpicturemethod-to-thecategoriestableadapter"></a>Krok 1: Přidání metody`InsertWithPicture`do`CategoriesTableAdapter`

Když jsme vytvořili `CategoriesTableAdapter` zpátky v kurzu [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-cs.md) , nakonfigurovali jsme ji tak, aby na základě hlavního dotazu automaticky generovala příkazy `INSERT`, `UPDATE`a `DELETE`. Kromě toho jsme TableAdapteri, že používá přímý přístup k databázi, který vytvořil metody `Insert`, `Update`a `Delete`. Tyto metody spouštějí automaticky generované `INSERT`, `UPDATE`a `DELETE` příkazy a následně přijímají vstupní parametry založené na sloupcích vrácených hlavním dotazem. V kurzu [nahrávání souborů](uploading-files-cs.md) jsme vylepšili hlavní dotaz `CategoriesTableAdapter` s pro použití sloupce `BrochurePath`.

Vzhledem k tomu, že hlavní dotaz `CategoriesTableAdapter` s neodkazuje na sloupec `Picture`, nemůžeme přidat nový záznam ani aktualizovat existující záznam s hodnotou sloupce `Picture`. Aby bylo možné zachytit tyto informace, můžeme buď vytvořit novou metodu v TableAdapter, která se používá speciálně pro vložení záznamu s binárními daty, nebo můžeme přizpůsobit automaticky generovaný `INSERT` příkaz. Problém s přizpůsobením automaticky generovaného příkazu `INSERT` je to, že riskujeme, že naše přizpůsobení přepsal průvodcem. Představte si například, že jsme přizpůsobili příkaz `INSERT`, aby zahrnoval použití `Picture` sloupce. Tím se aktualizuje metoda TableAdapter s `Insert` tak, aby zahrnovala další vstupní parametr pro binární data kategorie s obrázku. Pak můžeme vytvořit metodu v vrstvě obchodní logiky, která použije tuto metodu DAL, a vyvolat tuto metodu knihoven BLL prostřednictvím prezentační vrstvy a vše by fungovalo velmi dokonalé. To znamená, až do příštího nakonfigurovaného TableAdapter prostřednictvím Průvodce konfigurací TableAdapter. Jakmile se průvodce dokončí, naše přizpůsobení `INSERT` příkazu by se přepsaly, `Insert` metoda by se vrátila do původní formy a náš kód by se už nekompiluje!

> [!NOTE]
> Nejedná se o problém při použití uložených procedur místo ad-hoc příkazů SQL. V budoucím kurzu se místo ad-hoc příkazů SQL ve vrstvě přístupu k datům podíváme na použití uložených procedur.

Aby se zabránilo tomuto potenciálnímu starostí, nemusíte místo přizpůsobení automaticky generovaných příkazů SQL vytvořit novou metodu pro TableAdapter. Tato metoda s názvem `InsertWithPicture`akceptuje hodnoty pro sloupce `CategoryName`, `Description`, `BrochurePath`a `Picture` a spustí příkaz `INSERT`, který ukládá všechny čtyři hodnoty do nového záznamu.

Otevřete typovou datovou sadu a v návrháři klikněte pravým tlačítkem myši na záhlaví `CategoriesTableAdapter` s a v místní nabídce vyberte možnost Přidat dotaz. Tím se spustí Průvodce konfigurací dotazu TableAdapter, který začíná dotazem, jak by měl dotaz TableAdapter získat přístup k databázi. Vyberte možnost použít příkazy jazyka SQL a klikněte na tlačítko Další. V dalším kroku se zobrazí výzva k zadání typu dotazu, který se má vygenerovat. Vzhledem k tomu, že jsme znovu vytvořili dotaz pro přidání nového záznamu do tabulky `Categories`, vyberte možnost Vložit a klikněte na tlačítko Další.

[![vyberte možnost vložení.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.png)

**Obrázek 1**: vyberte možnost vložení ([kliknutím zobrazíte obrázek v plné velikosti](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.png)).

Teď je potřeba zadat příkaz `INSERT` SQL. Průvodce automaticky navrhne `INSERT` příkaz, který odpovídá hlavnímu dotazu TableAdapter s. V tomto případě je to příkaz `INSERT`, který vloží hodnoty `CategoryName`, `Description`a `BrochurePath`. Aktualizujte příkaz tak, aby byl zahrnutý `Picture` sloupec společně s parametrem `@Picture`, například takto:

[!code-sql[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample1.sql)]

Poslední obrazovka průvodce vás požádá o pojmenování nové metody TableAdapter. Zadejte `InsertWithPicture` a klikněte na Dokončit.

[![název novou metodu TableAdapter InsertWithPicture](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.png)

**Obrázek 2**: pojmenování nové metody TableAdapter `InsertWithPicture` ([kliknutím zobrazíte obrázek v plné velikosti](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.png))

## <a name="step-2-updating-the-business-logic-layer"></a>Krok 2: aktualizace vrstvy obchodní logiky

Vzhledem k tomu, že prezentační vrstva by měla pouze rozhraní s vrstvou obchodní logiky, než ji obejít a přejít přímo do vrstvy přístupu k datům, musíme vytvořit metodu knihoven BLL, která vyvolá metodu DAL, kterou jsme právě vytvořili (`InsertWithPicture`). Pro tento kurz vytvořte metodu ve třídě `CategoriesBLL` s názvem `InsertWithPicture`, která přijímá jako vstup tři `string` s a pole `byte`. Vstupní parametry `string` jsou pro název kategorie, popis a cestu k souboru brožury, zatímco `byte` pole je pro binární obsah obrázku kategorie s. Jak ukazuje následující kód, tato metoda knihoven BLL vyvolá odpovídající metodu DAL:

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample2.cs)]

> [!NOTE]
> Před přidáním metody `InsertWithPicture` do knihoven BLL se ujistěte, že jste uložili typovou datovou sadu. Vzhledem k tomu, že se kód třídy `CategoriesTableAdapter` automaticky generuje na základě typované datové sady, pokud nechcete nejdřív Uložit změny do typované datové sady, nebude mít vlastnost `Adapter` informace o metodě `InsertWithPicture`.

## <a name="step-3-listing-the-existing-categories-and-their-binary-data"></a>Krok 3: výpis stávajících kategorií a jejich binárních dat

V tomto kurzu vytvoříme stránku, která umožní koncovému uživateli přidat do systému novou kategorii a zadat obrázek a brožuru pro novou kategorii. V [předchozím kurzu](displaying-binary-data-in-the-data-web-controls-cs.md) jsme použili prvek GridView s vlastností TemplateField a ImageField k zobrazení jednotlivých kategorií s názvem, popisem, obrázkem a odkazem ke stažení jeho brožury. Tuto funkci je možné replikovat pro tento kurz, takže se vytvoří stránka, která bude obsahovat seznam všech existujících kategorií a umožní vytváření nových.

Začněte tím, že otevřete stránku `DisplayOrDownload.aspx` ze složky `BinaryData`. Přejít do zobrazení zdroje a zkopírovat deklarativní syntaxi GridView a ObjectDataSource s a vložit do prvku `<asp:Content>` v `UploadInDetailsView.aspx`. Také nenezapomeňte kopírovat přes `GenerateBrochureLink` metodu z třídy kódu na pozadí `DisplayOrDownload.aspx` na `UploadInDetailsView.aspx`.

[![zkopírování a vložení deklarativní syntaxe ze DisplayOrDownload. aspx do UploadInDetailsView. aspx.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.png)

**Obrázek 3**: zkopírování a vložení deklarativní syntaxe z `DisplayOrDownload.aspx` do `UploadInDetailsView.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.png))

Po zkopírování deklarativní syntaxe a metody `GenerateBrochureLink` do stránky `UploadInDetailsView.aspx` zobrazte stránku pomocí prohlížeče, aby bylo zajištěno, že vše bylo zkopírováno správně. Měl by se zobrazit prvek GridView obsahující osm kategorií, které obsahují odkaz ke stažení brožury a také obrázek kategorie s.

[![by se teď měla zobrazit každá kategorie spolu s jejich binárními daty.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.png)

**Obrázek 4**: teď byste měli vidět jednotlivé kategorie spolu s jejími binárními daty ([kliknutím zobrazíte obrázek v plné velikosti).](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.png)

## <a name="step-4-configuring-thecategoriesdatasourceto-support-inserting"></a>Krok 4: Konfigurace`CategoriesDataSource`pro podporu vložení

`CategoriesDataSource` ObjectDataSource, kterou používá `Categories` GridView, aktuálně neposkytuje možnost vkládat data. Aby bylo možné podporovat vkládání prostřednictvím tohoto ovládacího prvku zdroje dat, musíme namapovat svou `Insert` metodu na metodu v podkladovém objektu, `CategoriesBLL`. Konkrétně je chceme namapovat na `CategoriesBLL` metodu, kterou jsme přidali zpátky v kroku 2, `InsertWithPicture`.

Začněte tím, že kliknete na odkaz konfigurace zdroje dat z inteligentní značky ObjectDataSource s. Na první obrazovce se zobrazuje objekt, se kterým je zdroj dat nakonfigurován pro práci s `CategoriesBLL`. Toto nastavení nechte beze změny a kliknutím na tlačítko Další přejděte na obrazovku definovat metody dat. Přejděte na kartu Vložení a v rozevíracím seznamu vyberte metodu `InsertWithPicture`. Kliknutím na Dokončit dokončete průvodce.

[![nakonfigurovat prvek ObjectDataSource na použití metody InsertWithPicture](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.png)

**Obrázek 5**: Konfigurace prvku ObjectDataSource pro použití metody `InsertWithPicture` ([kliknutím zobrazíte obrázek v plné velikosti](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.png))

> [!NOTE]
> Po dokončení průvodce může Visual Studio požádat, zda chcete aktualizovat pole a klíče, čímž dojde k opětovnému vygenerování polí webové ovládací prvky dat. Zvolte možnost Ne, protože výběrem možnosti Ano dojde k přepsání všech úprav polí, které jste mohli udělat.

Po dokončení průvodce prvek ObjectDataSource nyní zahrne hodnotu pro vlastnost `InsertMethod` a také `InsertParameters` pro sloupce čtyř kategorií, jak ukazuje následující deklarativní kód:

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample3.aspx)]

## <a name="step-5-creating-the-inserting-interface"></a>Krok 5: vytvoření rozhraní pro vložení

Jak je uvedeno v [přehledu o vkládání, aktualizaci a odstraňování dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md), ovládací prvek DetailsView poskytuje integrované rozhraní pro vložení, které lze využít při práci s ovládacím prvkem zdroje dat, který podporuje vkládání. Do této stránky přidejte ovládací prvek DetailsView nad prvek GridView, který bude trvale vykreslovat rozhraní pro vložení, což uživateli umožňuje rychle přidat novou kategorii. Po přidání nové kategorie v ovládacím prvku DetailsView se prvek GridView pod ním automaticky aktualizuje a zobrazí novou kategorii.

Začněte přetažením prvku DetailsView z panelu nástrojů do návrháře nad ovládací prvek GridView, nastavením jeho vlastnosti `ID` na `NewCategory` a vymazáním hodnot vlastností `Height` a `Width`. Z inteligentní značky DetailsView s vytvořte vazby na existující `CategoriesDataSource` a zaškrtněte políčko Povolit vložení.

[![Přivážete prvek DetailsView k CategoriesDataSource a povolit vkládání](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.png)

**Obrázek 6**: Svázání prvku DetailsView s `CategoriesDataSource` a povolení vložení ([kliknutím zobrazíte obrázek v plné velikosti](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image12.png))

Chcete-li prvek DetailsView trvale vykreslit v rozhraní pro vložení, nastavte jeho vlastnost `DefaultMode` na hodnotu `Insert`.

Všimněte si, že prvek DetailsView má pět BoundFields `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`a `BrochurePath` i když se `CategoryID` vlastnost BoundField nevykresluje v rozhraní pro vložení, protože jeho vlastnost `InsertVisible` je nastavená na `false`. Tyto BoundFields existují, protože jsou sloupce vracené metodou `GetCategories()`, což je to, co prvek ObjectDataSource vyvolá k načtení dat. Pro vložení ale nechcete, aby uživatel mohl zadat hodnotu pro `NumberOfProducts`. Kromě toho je potřeba jim dovolit, aby nahráli obrázek pro novou kategorii a nahráli PDF pro brožuru.

Odeberte `NumberOfProducts` vlastnost BoundField z ovládacího prvku DetailsView a pak aktualizujte `HeaderText` vlastnosti `CategoryName` a `BrochurePath` BoundFields na kategorii a brožuru v uvedeném pořadí. Dále převeďte `BrochurePath` vlastnost BoundField na TemplateField a přidejte nové pole TemplateField pro obrázek, čímž tuto novou hodnotu TemplateField `HeaderText` obrázku. Přesuňte pole `Picture` TemplateField tak, aby bylo mezi `BrochurePath` TemplateField a CommandField.

![Navázání prvku DetailsView na CategoriesDataSource a povolení vložení](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.gif)

**Obrázek 7**: Svázání prvku DetailsView s `CategoriesDataSource` a povolení vložení

Pokud jste převedli `BrochurePath` vlastnost BoundField na TemplateField prostřednictvím dialogového okna Upravit pole, pole TemplateField zahrnuje `ItemTemplate`, `EditItemTemplate`a `InsertItemTemplate`. Je ale potřeba, abyste ale mohli odebrat i ostatní dvě šablony, ale nebudete mít k dispozici jenom `InsertItemTemplate`. V tomto okamžiku by deklarativní syntaxe ovládacího prvku DetailsView s vypadala takto:

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample4.aspx)]

## <a name="adding-fileupload-controls-for-the-brochure-and-picture-fields"></a>Přidání ovládacích prvků nahrání souborů pro brožuru a pole obrázků

V předposílání `BrochurePath` TemplateField s `InsertItemTemplate` obsahuje textové pole, zatímco `Picture` TemplateField neobsahuje žádné šablony. Abychom mohli použít ovládací prvky pro nahrání souborů, musíme tyto dvě `InsertItemTemplate`y TemplateField aktualizovat.

Z inteligentní značky DetailsView s zvolte možnost Upravit šablony a potom v rozevíracím seznamu vyberte `InsertItemTemplate` `BrochurePath` TemplateField s. Odeberte textové pole a přetáhněte ovládací prvek pro nahrání souborů ze sady nástrojů do šablony. Nastavte `ID` ovládacího prvku pro nahrání souboru s `BrochureUpload`. Podobně přidejte ovládací prvek pro nahrání souborů do `Picture` TemplateField s `InsertItemTemplate`. Nastavte tuto `ID` ovládacího prvku pro nahrání souborů na `PictureUpload`.

[![přidat ovládací prvek pro nahrání souborů do šablona InsertItemTemplate](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image13.png)

**Obrázek 8**: Přidání ovládacího prvku pro nahrání souborů do `InsertItemTemplate` ([kliknutím zobrazíte obrázek v plné velikosti](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image14.png))

Po provedení těchto dodatků bude tato dvě deklarativní syntaxe ' TemplateField s ':

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample5.aspx)]

Když uživatel přidá novou kategorii, chceme zajistit, aby byla brožura a obrázek správného typu souboru. V případě brožury musí uživatel dodat soubor PDF. Pro obrázek potřebujeme, aby uživatel nahrál soubor s obrázkem, ale povolili jsme *jakýkoliv* soubor obrázku nebo jenom soubory obrázků určitého typu, jako je GIF nebo JPGs? Aby bylo možné použít různé typy souborů, potřebujeme, abyste rozšířili schéma `Categories`, aby zahrnovalo sloupec, který zachytává typ souboru, aby se tento typ mohl odeslat klientovi prostřednictvím `Response.ContentType` v `DisplayCategoryPicture.aspx`. Vzhledem k tomu, že tento sloupec nepoužíváme, by byl obezřetný, aby bylo možné omezit uživatelům pouze zadání konkrétního typu souboru obrázku. Existující image `Categories` tabulky jsou rastrové obrázky, ale JPGs jsou vhodnější formát souboru pro obrázky, které jsou obsluhovány na webu.

Pokud uživatel nahraje nesprávný typ souboru, musíme zrušit vložení a zobrazit zprávu s informacemi o problému. Přidejte ovládací prvek popisek webu pod ovládacím prvkem DetailsView. Vlastnost `ID` nastavte na `UploadWarning`, vymažte vlastnost `Text`, nastavte vlastnost `CssClass` na Warning a `Visible` a `EnableViewState` vlastnosti na `false`. `Warning` Třída CSS je definována v `Styles.css` a vykresluje text ve velkém, červeném, kurzívě tučném písmu.

> [!NOTE]
> V ideálním případě se `CategoryName` a `Description` BoundFields převede na pole TemplateField a přizpůsobená rozhraní pro vložení. Rozhraní `Description` pro vložení například by pravděpodobně lépe vyhovovalo víceřádkovým textovým polem. A vzhledem k tomu, že `CategoryName` sloupec nepřijímá `NULL` hodnoty, měla by být přidána RequiredFieldValidator, která zajistí, že uživatel zadá hodnotu pro nový název kategorie. Tento postup je ponechán jako cvičení pro čtenáře. Přečtěte si další informace k [přizpůsobení rozhraní pro úpravu dat](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) pro podrobnější pohled na rozšíření rozhraní pro úpravu dat.

## <a name="step-6-saving-the-uploaded-brochure-to-the-web-server-s-file-system"></a>Krok 6: uložení nahrané brožury do systému souborů webového serveru s

Když uživatel zadá hodnoty do nové kategorie a klikne na tlačítko Vložit, dojde k postbacku a vložení pracovního postupu. Nejprve se aktivuje [událost`ItemInserting`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserting.aspx) ovládacího prvku. Dále je vyvolána metoda ObjectDataSource s `Insert()`, což vede k přidání nového záznamu do tabulky `Categories`. Poté je aktivována událost DetailsView s [`ItemInserted`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserted.aspx) .

Před vyvoláním metody ObjectDataSource `Insert()` je třeba nejprve zkontrolovat, že uživatel nahrál příslušné typy souborů a pak uložit brožuru PDF do systému souborů webového serveru s. Vytvořte obslužnou rutinu události pro událost DetailsView s `ItemInserting` a přidejte následující kód:

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample6.cs)]

Obslužná rutina události začíná odkazem na ovládací prvek nahrání `BrochureUpload` ze šablon ovládacího prvku DetailsView s. Až se nahrála brožura, nahraná Přípona souboru s se vyšetří. Pokud rozšíření není. PDF, zobrazí se upozornění, vložení se zruší a spuštění obslužné rutiny události skončí.

> [!NOTE]
> Spoléhání se na nahrané rozšíření souboru s není jistou technikou, aby bylo zajištěno, že nahraný soubor je dokument PDF. Uživatel může mít platný dokument PDF s rozšířením `.Brochure`, nebo mohl vytvořit dokument, který není v PDF, a udělit mu `.pdf` rozšíření. Binární obsah souboru s by se musel programově prozkoumat, aby bylo možné tento typ souboru ještě neprůkazně ověřit. Takové důkladné přístupy se sice často přehnaně důkladné; Kontrola rozšíření je pro většinu scénářů dostačující.

Jak je popsáno v kurzu při [nahrávání souborů](uploading-files-cs.md) , je potřeba při ukládání souborů do systému souborů dbát na to, aby jeden uživatel s nahráváním nepřepisoval další s. V tomto kurzu se pokusíme použít stejný název jako nahraný soubor. Pokud již existuje soubor v adresáři `~/Brochures` se stejným názvem souboru, přidáme číslo na konci, dokud nebude nalezen jedinečný název. Například pokud uživatel nahraje soubor brožury s názvem `Meats.pdf`, ale ve složce `~/Brochures` již existuje soubor s názvem `Meats.pdf`, změníme název uloženého souboru na `Meats-1.pdf`. Pokud existuje, zkusíme `Meats-2.pdf`a tak dále, dokud se nenajde jedinečný název souboru.

Následující kód používá [metodu`File.Exists(path)`](https://msdn.microsoft.com/library/system.io.file.exists.aspx) k určení, zda soubor se zadaným názvem souboru již existuje. Pokud ano, bude i nadále zkoušet nové názvy souborů pro brožuru, dokud nebude nalezen žádný konflikt.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample7.cs)]

Jakmile bude nalezen platný název souboru, je třeba soubor uložit do systému souborů a prvek ObjectDataSource `brochurePath``InsertParameter` musí být aktualizován, aby byl tento název souboru zapsán do databáze. Jak jsme se v kurzu *nahrávání souborů* viděli zpátky, soubor se dá uložit pomocí `SaveAs(path)` metoda nahrání souboru s. Chcete-li aktualizovat parametr ObjectDataSource s `brochurePath`, použijte kolekci `e.Values`.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample8.cs)]

## <a name="step-7-saving-the-uploaded-picture-to-the-database"></a>Krok 7: uložení nahraného obrázku do databáze

Abychom uložili nahraný obrázek do nového záznamu `Categories`, musíme nahraného binárního obsahu přiřadit parametru ObjectDataSource s `picture` v události DetailsView s `ItemInserting`. Než začneme s tímto přiřazením, musíme nejdřív zkontrolovat, že nahraný obrázek je JPG, a ne jiný typ obrázku. Jak je uvedeno v kroku 6, pomocí nahraného souboru s obrázkem s můžete zjistit jeho typ.

Zatímco tabulka `Categories` umožňuje `NULL` hodnoty pro sloupec `Picture`, všechny kategorie nyní mají obrázek. Pojďme uživateli přinutit, aby při přidávání nové kategorie přes tuto stránku zadali obrázek. Následující kód zkontroluje, zda byl obrázek nahrán a zda má odpovídající rozšíření.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample9.cs)]

Tento kód by měl být umístěn *před* kódem z kroku 6, aby v případě, že dojde k potížím s nahráváním obrázku, obslužná rutina události skončí před uložením souboru brožury do systému souborů.

Za předpokladu, že byl nahrán příslušný soubor, přiřaďte nahraný binární obsah k hodnotě parametru obrázku s následujícím řádkem kódu:

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample10.cs)]

## <a name="the-completeiteminsertingevent-handler"></a>Kompletní obslužná rutina události`ItemInserting`

V případě úplnost je zde `ItemInserting` obslužná rutina události v celém rozsahu:

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample11.cs)]

## <a name="step-8-fixing-thedisplaycategorypictureaspxpage"></a>Krok 8: Oprava stránky`DisplayCategoryPicture.aspx`

Počkejte chvilku, než se otestuje rozhraní pro vložení rozhraní a `ItemInserting` obslužnou rutinu, která se vytvořila během posledních několika kroků. Přejděte na stránku `UploadInDetailsView.aspx` v prohlížeči a pokuste se přidat kategorii, ale vynechejte obrázek nebo zadejte obrázek, který není typu JPG, nebo brožuru, která není ve formátu PDF. V některých případech se zobrazí chybová zpráva a pracovní postup vložení byl zrušen.

[![se zobrazí zpráva s upozorněním, pokud se nahraje neplatný typ souboru.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image15.png)

**Obrázek 9**: při odeslání neplatného typu souboru se zobrazí zpráva s upozorněním ([kliknutím zobrazíte obrázek v plné velikosti).](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image16.png)

Jakmile ověříte, že stránka vyžaduje nahrávání obrázku a nepřijímá soubory ve formátu PDF ani jiné než JPG, přidejte novou kategorii s platným obrázkem JPG a nechejte pole brožura prázdné. Po kliknutí na tlačítko Vložit se stránka odešle zpět a nový záznam se přidá do tabulky `Categories` s nahraným binárním obsahem obrázků s uloženými přímo v databázi. Prvek GridView se aktualizuje a zobrazí řádek pro nově přidanou kategorii, ale na obrázku 10 se zobrazí nový obrázek kategorie není správně vykreslen.

[![se nový obrázek kategorie nezobrazí.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image17.png)

**Obrázek 10**: obrázek nové kategorie není zobrazený ([kliknutím zobrazíte obrázek v plné velikosti).](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image18.png)

Důvod, proč se nový obrázek nezobrazuje, je, že `DisplayCategoryPicture.aspx` stránka, která vrací zadaný obrázek kategorie s, je nakonfigurována pro zpracování rastrových obrázků, které mají hlavičku OLE. Tato hlavička bajtu 78 se před odesláním zpátky klientovi vrátí z binárního obsahu `Picture`ového sloupce. Ale soubor s příponou. JPG, který jsme právě Nahráli pro novou kategorii, nemá tuto hlavičku OLE. Proto jsou z binárních dat image s odebírány platné bajty, které jsou nezbytné.

Vzhledem k tomu, že jsou teď v tabulce `Categories` obě bitmapy s hlavičkou OLE a JPGs, musíme aktualizovat `DisplayCategoryPicture.aspx` tak, aby se vynechá vyřazení hlaviček OLE pro původní osm kategorií, a obejít tuto úpravu pro novější záznamy kategorií. V našem dalším kurzu probereme, jak aktualizovat existující image záznamu a aktualizujeme všechny staré obrázky kategorií, aby byly JPGs. Teď ale použijte následující kód v `DisplayCategoryPicture.aspx` k obložení hlaviček OLE jenom pro tyto původní osm kategorií:

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample12.cs)]

Tato změna znamená, že obrázek JPG je nyní vykreslen správně v prvku GridView.

[![obrázků JPG pro nové kategorie se správně vykreslí.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image19.png)

**Obrázek 11**: obrázky ve formátu jpg pro nové kategorie jsou správně vykresleny ([kliknutím zobrazíte obrázek v plné velikosti).](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image20.png)

## <a name="step-9-deleting-the-brochure-in-the-face-of-an-exception"></a>Krok 9: odstranění brožury na straně výjimky

Jedním z výzev k ukládání binárních dat do systému souborů webového serveru s je, že zavádí odpojení mezi datovým modelem a jeho binárními daty. Proto se při každém odstranění záznamu musí odebrat i odpovídající binární data v systému souborů. To může přijít do hry i při vkládání. Vezměte v úvahu následující scénář: uživatel přidá novou kategorii a určí platný obrázek a brožuru. Po kliknutí na tlačítko Vložit dojde k postbacku a událost ovládacího prvku DetailsView `ItemInserting` se aktivuje a uloží brožuru do systému souborů webového serveru s. Dále je vyvolána metoda ObjectDataSource s `Insert()`, která volá metodu `InsertWithPicture` `CategoriesBLL` třídy s, která volá metodu `InsertWithPicture` `CategoriesTableAdapter` s.

Co se stane, když je databáze offline, nebo pokud v příkazu `INSERT` SQL dojde k chybě? Jasně se vložení nezdaří, takže do databáze se nepřidá žádný nový řádek kategorie. Ale pořád máme nahraný soubor brožury v systému souborů webového serveru s! Tento soubor je nutné odstranit na straně výjimky během vkládání pracovního postupu.

Jak bylo popsáno dříve v kurzu [zpracování knihoven BLL a na úrovni dal v kurzu stránky ASP.NET](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) , pokud je vyvolána výjimka v rámci hloubky architektury, která je seznáma prostřednictvím různých vrstev. V prezentační vrstvě můžeme určit, zda došlo k výjimce z události `ItemInserted` ovládacího prvku. Tato obslužná rutina události také poskytuje hodnoty `InsertParameters`ObjectDataSource s. Proto můžeme vytvořit obslužnou rutinu události pro událost `ItemInserted`, která kontroluje, zda došlo k výjimce, a pokud ano, odstraní soubor určený parametrem ObjectDataSource s `brochurePath`:

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample13.cs)]

## <a name="summary"></a>Přehled

K dispozici je řada kroků, které je třeba provést, aby bylo možné poskytovat webové rozhraní pro přidávání záznamů, které zahrnují binární data. Pokud jsou binární data ukládána přímo do databáze, je pravděpodobné, že budete muset aktualizovat architekturu a přidat konkrétní metody, které budou zpracovávat případy, kdy jsou vložena binární data. Po aktualizaci architektury je dalším krokem vytvoření rozhraní pro vložení, které lze provést pomocí ovládacího prvku DetailsView, který je přizpůsobený tak, aby zahrnoval ovládací prvek nahrání souboru pro každé binární datové pole. Nahraná data je pak možné uložit do systému souborů webového serveru s nebo přiřadit k parametru zdroje dat v obslužné rutině ovládacího prvku DetailsView s `ItemInserting`.

Ukládání binárních dat do systému souborů vyžaduje více plánování než ukládání dat přímo do databáze. Aby bylo možné zabránit jednomu uživateli v zápisu dalších souborů, je třeba zvolit schéma pojmenování. V případě, že se vložení databáze nepovede, je třeba provést další kroky, aby se nahraný soubor odstranil.

Teď máme možnost přidat do systému nové kategorie s brožurou a obrázkem, ale zatím jsme si vyhledali, jak aktualizovat existující binární data v kategorii nebo jak správně odebrat binární data pro odstraněnou kategorii. Tato dvě témata prozkoumáme v dalším kurzu.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Dave Gardner, Teresa Murphy a Bernadette Leigh. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](displaying-binary-data-in-the-data-web-controls-cs.md)
> [Další](updating-and-deleting-existing-binary-data-cs.md)

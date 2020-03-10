---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs
title: Přehled úprav a odstranění dat v prvku DataList (C#) | Microsoft Docs
author: rick-anderson
description: I když prvek DataList nemá integrované možnosti úprav a odstranění, v tomto kurzu se dozvíte, jak vytvořit prvek DataList, který podporuje úpravy a odstranění o...
ms.author: riande
ms.date: 10/30/2006
ms.assetid: c3b0c86e-fe98-41ee-b26f-ca38cddaa75e
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 481c9a14b1ebfe36ffcddd0237701bc04266e393
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78594554"
---
# <a name="an-overview-of-editing-and-deleting-data-in-the-datalist-c"></a>Přehled úprav a odstranění dat v prvku DataList (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_36_CS.exe) nebo [Stáhnout PDF](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/datatutorial36cs1.pdf)

> I když prvek DataList nemá integrované možnosti úprav a odstranění, v tomto kurzu se dozvíte, jak vytvořit prvek DataList, který podporuje úpravy a odstraňování svých podkladových dat.

## <a name="introduction"></a>Úvod

V [přehledu vložení, aktualizace a odstranění dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) jsme se podívali na to, jak vkládat, aktualizovat a odstraňovat data pomocí architektury aplikace, prvku ObjectDataSource a ovládacích prvků GridView, DetailsView a FormView. V prvku ObjectDataSource a těchto třech webových ovládacích prvcích dat byla implementace jednoduchých rozhraní pro úpravu dat přichycena a zapojena pouze do zaškrtávacího políčka z inteligentní značky. Není nutné psát žádný kód.

Rozhraní DataList bohužel nemá integrované možnosti úprav a odstranění, které jsou součástí ovládacího prvku GridView. Tato chybějící funkce je způsobena součástí faktu, že prvek DataList je Relic z předchozí verze ASP.NET, když ovládací prvky deklarativního zdroje dat a stránky pro úpravu dat bez kódu nejsou k dispozici. I když DataList v ASP.NET 2,0 nenabízí stejné možnosti změny dat jako v prvku GridView, můžeme použít techniky ASP.NET 1. x k zahrnutí takových funkcí. Tento přístup vyžaduje bitovou kopii, ale v tomto kurzu bude mít prvek DataList v tomto procesu k dispozici několik událostí a vlastností, které by měly pomoci.

V tomto kurzu se dozvíte, jak vytvořit prvek DataList, který podporuje úpravy a odstraňování svých podkladových dat. Budoucí kurzy prozkoumají pokročilejší úpravy a odstraňování scénářů, včetně ověřování vstupního pole, a řádným zpracování výjimek vyvolaných z vrstev přístupu k datům nebo obchodní logiky atd.

> [!NOTE]
> Podobně jako u prvku DataList nemá ovládací prvek Repeater dostatek funkcí pro vložení, aktualizaci nebo odstranění. I když je možné tyto funkce Přidat, DataList zahrnuje vlastnosti a události, které se nenašly v OPAKOVAČI, které zjednodušují přidávání takových možností. Proto tento kurz a budoucí, které vypadají při úpravách a odstraňování, se budou přesně zaměřit na prvky DataList.

## <a name="step-1-creating-the-editing-and-deleting-tutorials-web-pages"></a>Krok 1: vytvoření webových stránek s pokyny k úpravám a odstraňování

Předtím, než začneme zkoumat, jak aktualizovat a odstraňovat data z prvku DataList, si nejdřív vydejte chvilku, abyste vytvořili stránky ASP.NET v našem projektu webu, který budeme potřebovat pro tento kurz a další. Začněte přidáním nové složky s názvem `EditDeleteDataList`. Dále přidejte následující stránky ASP.NET do této složky a nezapomeňte přidružit jednotlivé stránky k `Site.master` hlavní stránce:

- `Default.aspx`
- `Basics.aspx`
- `BatchUpdate.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![Přidání stránek ASP.NET pro kurzy](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image1.png)

**Obrázek 1**: přidání stránek ASP.NET pro kurzy

Podobně jako v ostatních složkách `Default.aspx` ve složce `EditDeleteDataList` seznam kurzů v příslušné části. Zajistěte, aby tato funkce poskytovala `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek. Proto tento uživatelský ovládací prvek přidejte do `Default.aspx` tím, že ho přetáhnete z Průzkumník řešení na zobrazení Návrh stránky.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image3.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image2.png)

**Obrázek 2**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image4.png))

Nakonec přidejte stránky jako položky do souboru `Web.sitemap`. Konkrétně přidejte následující značky za hlavní a podrobné sestavy pomocí ovládacího prvku DataList a Repeater `<siteMapNode>`:

[!code-xml[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample1.xml)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. Nabídka na levé straně teď obsahuje položky pro kurzy upravující a odstraňování DataList.

![Mapa webu teď obsahuje položky pro kurzy pro úpravy a odstraňování DataList.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image5.png)

**Obrázek 3**: Mapa webu teď obsahuje položky pro kurzy pro úpravy a odstraňování v DataList.

## <a name="step-2-examining-techniques-for-updating-and-deleting-data"></a>Krok 2: zkoumání techniků pro aktualizaci a odstraňování dat

Úpravy a odstranění dat pomocí prvku GridView je tak snadné, protože pod sebou jsou v prvku GridView a ObjectDataSource spolupracuje. Jak je popsáno v tématu [zkoumání událostí souvisejících s vložením, aktualizací a odstraněním](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) kurzu, při kliknutí na tlačítko Aktualizovat řádek, ovládací prvek GridView automaticky přiřadí jeho pole, které použily obousměrnou datovou vazbu do kolekce `UpdateParameters` svého prvku ObjectDataSource a poté vyvolá tuto `Update()` metodu ObjectDataSource.

Bohužel, DataList neposkytuje žádnou z těchto integrovaných funkcí. Je naše zodpovědnost za to, že jsou hodnoty uživatele přiřazeny parametrům ObjectDataSource s a že je volána jeho `Update()` metoda. Abychom nám mohli pomoci v tomto Endeavor, poskytuje prvek DataList následující vlastnosti a události:

- **[Vlastnost`DataKeyField`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeyfield.aspx)** při aktualizaci nebo odstranění musíme být schopni jednoznačně identifikovat každou položku v prvku DataList. Nastavte tuto vlastnost na pole primární klíč zobrazených dat. Tím dojde k naplnění [kolekce`DataKeys`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeys.aspx) DataList s zadanou `DataKeyField` hodnotou pro každou položku prvku DataList.
- **[Událost`EditCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.editcommand.aspx)** je aktivována při kliknutí na tlačítko, LinkButton nebo obrázkové, jejichž vlastnost `CommandName` je nastavena na hodnotu upravit.
- **[Událost`CancelCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.cancelcommand.aspx)** je aktivována při kliknutí na tlačítko, LinkButton nebo obrázkové, jejichž vlastnost `CommandName` je nastavena na hodnotu Storno.
- **[Událost`UpdateCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.updatecommand.aspx)** je aktivována při kliknutí na tlačítko, LinkButton nebo obrázkové, jejichž vlastnost `CommandName` je nastavena na hodnotu aktualizovat.
- **[Událost`DeleteCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.deletecommand.aspx)** je aktivována při kliknutí na tlačítko, LinkButton nebo obrázkové, jejichž vlastnost `CommandName` je nastavena na hodnotu odstranit.

Pomocí těchto vlastností a událostí můžete k aktualizaci a odstraňování dat z prvku DataList použít čtyři způsoby:

1. **Pomocí ASP.NET 1. x techniky** DataList existovalo před ASP.NET 2,0 a prvky ObjectDataSource a bylo možné aktualizovat a odstranit data výhradně prostřednictvím programových prostředků. Tato technika ditches prvek ObjectDataSource zcela a vyžaduje, aby se data navázala přímo z vrstvy obchodní logiky při načítání dat k zobrazení a při aktualizaci nebo odstranění záznamu.
2. **Použití jednoho ovládacího prvku ObjectDataSource na stránce pro výběr, aktualizaci a odstranění** , zatímco v prvku DataList chybí prvek GridView s podstatou možností úprav a odstranění, neexistuje žádný důvod, proč je můžeme přidat do dodržovali. S tímto přístupem používáme prvek ObjectDataSource stejně jako v příkladech GridView, ale musí vytvořit obslužnou rutinu události pro `UpdateCommand` událost DataList s, kde nastavíme parametry ObjectDataSource s a zavolejte metodu `Update()`.
3. **Pomocí ovládacího prvku ObjectDataSource pro výběr, ale aktualizace a odstranění přímo proti knihoven BLL** při použití možnosti 2, musíme napsat bitovou část kódu v události `UpdateCommand`, přiřadit hodnoty parametrů atd. Místo toho můžeme použít ovládací prvek ObjectDataSource pro výběr, ale provedení aktualizace a odstranění volání přímo proti knihoven BLL (jako s možností 1). Ve svém stanovisku aktualizace dat přímým přístupem s knihoven BLL vede k čitelnějšímu kódu, než přiřazení `UpdateParameters` ObjectDataSource s a volání metody `Update()`.
4. **Použití deklarativních prostředků prostřednictvím více prvků ObjectDataSource** všechny předchozí tři přístupy vyžadují bitovou část kódu. Pokud místo toho chcete dál používat co nejvíc deklarativní syntaxe, je finální volbou zahrnutí více prvků ObjectDataSource na stránce. První prvek ObjectDataSource načte data z knihoven BLL a váže ji k prvku DataList. Pro aktualizaci je přidána jiná ObjectDataSource, ale přidána přímo v rámci `EditItemTemplate`DataList. Chcete-li zahrnout podporu odstraňování, je v `ItemTemplate`potřeba ještě další prvek ObjectDataSource. S tímto přístupem tyto vložené prvky ObjectDataSource používají `ControlParameters` k deklarativnímu vázání parametrů ObjectDataSource s k ovládacím prvkům vstupu uživatele (místo nutnosti jejich zadání programově v obslužné rutině události `UpdateCommand` DataList). Tento přístup ještě vyžaduje bitovou kopii, musíme volat vložené prvky ObjectDataSource s `Update()` nebo `Delete()`, ale vyžaduje mnohem méně než u dalších tří přístupů. Nevýhodou tady je, že vícenásobné prvky ObjectDataSource neobsahují stránku na stránce a odvolávat z celkové čitelnosti.

Pokud je aplikace vynucená jenom v jednom z těchto přístupů, můžu mi vybrat možnost 1, protože poskytuje největší flexibilitu a vzhledem k tomu, že prvek DataList byl původně navržený tak, aby odpovídal tomuto vzoru. Přestože bylo rozšíření DataList rozšířeno na práci s ovládacími prvky zdroje dat ASP.NET 2,0, nemá všechny body rozšiřitelnosti ani funkce oficiálních webových ovládacích prvků ASP.NET 2,0 dat (GridView, DetailsView a FormView). Možnosti 2 až 4 nejsou bez skutkového nastavení, ale.

Toto a budoucí kurzy pro úpravy a odstraňování budou používat prvek ObjectDataSource k načtení dat k zobrazení a přímé volání knihoven BLL k aktualizaci a odstranění dat (možnost 3).

## <a name="step-3-adding-the-datalist-and-configuring-its-objectdatasource"></a>Krok 3: Přidání prvku DataList a konfigurace jeho prvku ObjectDataSource

V tomto kurzu vytvoříme prvek DataList, který obsahuje informace o produktech a pro každý produkt poskytuje uživateli možnost upravit si název a cenu a úplně odstranit produkt. Konkrétně načteme záznamy pro zobrazení pomocí prvku ObjectDataSource, ale akce aktualizace a odstranění provedete přímým přístupem k knihoven BLL. Předtím, než se obáváme o implementaci možností úprav a odstranění u prvku DataList, si nejdřív dejte stránku, aby se zobrazily produkty v rozhraní jen pro čtení. Vzhledem k tomu, že jsme prozkoumali tyto kroky v předchozích kurzech, provedete je rychle.

Začněte tím, že otevřete stránku `Basics.aspx` ve složce `EditDeleteDataList` a z zobrazení Návrh přidáte na stránku prvek DataList. Dále z inteligentní značky DataList s vytvořte nový prvek ObjectDataSource. Vzhledem k tomu, že pracujeme s daty produktu, nakonfigurujte ji tak, aby používala třídu `ProductsBLL`. Chcete-li načíst *všechny* produkty, zvolte na kartě vybrat metodu `GetProducts()`.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu ProductsBLL](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image7.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image6.png)

**Obrázek 4**: Konfigurace prvku ObjectDataSource, aby používal třídu `ProductsBLL` ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image8.png))

[![vrátit informace o produktu pomocí metody GetProducts ()](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image10.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image9.png)

**Obrázek 5**: vrácení informací o produktu pomocí metody `GetProducts()` ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image11.png))

Prvek DataList, například GridView, není navržen pro vkládání nových dat; z rozevíracího seznamu na kartě Vložit proto vyberte možnost (žádná). Pro karty UPDATE a DELETE také vyberte (žádné), protože aktualizace a odstranění se budou provádět programově prostřednictvím knihoven BLL.

[![potvrďte, že rozevírací seznamy v rámci karet ObjectDataSource s INSERT, UPDATE a DELETE jsou nastaveny na (žádné).](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image13.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image12.png)

**Obrázek 6**: potvrďte, že se rozevírací seznamy na kartách INSERT, Update a DELETE v prvku ObjectDataSource nastavily na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image14.png)

Po nakonfigurování prvku ObjectDataSource klikněte na tlačítko Dokončit a vraťte se do návrháře. Jak jsme viděli v minulých příkladech při dokončování konfigurace ObjectDataSource, Visual Studio automaticky vytvoří `ItemTemplate` pro DropDownList a zobrazí všechna datová pole. Nahraďte tuto `ItemTemplate` názvem, který zobrazuje pouze název a cenu produktu. Také nastavte vlastnost `RepeatColumns` na hodnotu 2.

> [!NOTE]
> Jak je popsáno v kurzu *vložení, aktualizace a odstranění dat* , při úpravě dat pomocí prvku ObjectDataSource naše architektura vyžaduje, abyste odebrali vlastnost `OldValuesParameterFormatString` z deklarativního označení ObjectDataSource s (nebo ji resetujete na výchozí hodnotu `{0}`). V tomto kurzu však používáme pro načítání dat pouze ObjectDataSource. Proto nemusíme upravovat hodnotu vlastnosti ObjectDataSource s `OldValuesParameterFormatString` (i když to nevede k tomu, že to nesnížit).

Po nahrazení výchozího `ItemTemplate` prvku DataList s přizpůsobeným použitím deklarativní značky na stránce by měly vypadat podobně jako následující:

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample2.aspx)]

Chvilku si můžete prohlédnout v prohlížeči. Jak ukazuje obrázek 7, prvek DataList zobrazuje název produktu a jednotkovou cenu pro každý produkt ve dvou sloupcích.

[![se názvy produktů a ceny zobrazují ve dvou sloupcích DataList](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image16.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image15.png)

**Obrázek 7**: názvy produktů a ceny se zobrazí ve dvou sloupcích DataList ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image17.png)).

> [!NOTE]
> Prvek DataList má řadu vlastností, které jsou požadovány pro proces aktualizace a odstranění, a tyto hodnoty jsou uloženy ve stavu zobrazení. Proto při sestavování prvku DataList, který podporuje úpravy nebo odstranění dat, je nezbytné, aby byl povolen stav zobrazení DataList s.  
>   
> Čtečka bystří může vyvolat, že při vytváření upravitelných prvků GridView, DetailsView a FormView jsme mohli zakázat stav zobrazení. Důvodem je, že webové ovládací prvky ASP.NET 2,0 mohou zahrnovat *stav ovládacího prvku*, který je trvale uložen napříč zpětnými odesláními, jako je například stav zobrazení, což se považuje za základní.

Zakázání stavu zobrazení v prvku GridView pouze vynechává informace o triviálním stavu, ale udržuje stav ovládacího prvku (který zahrnuje stav nutný pro úpravy a odstranění). Prvek DataList, který byl vytvořen v rámci časového rámce ASP.NET 1. x, nevyužívá stav ovládacího prvku, a proto musí mít povolený stav zobrazení. Další informace o účelu stavu ovládacího prvku a o tom, jak se liší od stavu zobrazení, naleznete v tématu [stav ovládacího prvku vs. zobrazení stavu](https://msdn.microsoft.com/library/1whwt1k7.aspx) .

## <a name="step-4-adding-an-editing-user-interface"></a>Krok 4: Přidání uživatelského rozhraní pro úpravy

Ovládací prvek GridView se skládá z kolekce polí (BoundFields, CheckBoxFields, TemplateFields atd.). Tato pole mohou upravit vykreslená označení v závislosti na jejich režimu. Například když v režimu jen pro čtení, vlastnost BoundField zobrazí hodnotu datového pole jako text; v režimu úprav vykreslí webový ovládací prvek TextBox, jehož vlastnost `Text` je přiřazena hodnota datového pole.

Prvek DataList na druhé straně vykresluje své položky pomocí šablon. Položky, které jsou jen pro čtení, se vykreslují pomocí `ItemTemplate`, zatímco položky v režimu úprav se vykreslují prostřednictvím `EditItemTemplate`. V tomto okamžiku má naše DataList pouze `ItemTemplate`. Aby bylo možné podporovat funkce pro úpravu na úrovni položek, musíme přidat `EditItemTemplate`, který obsahuje značku, která se má zobrazit pro upravitelnou položku. Pro tento kurz použijeme webové ovládací prvky TextBox pro úpravu názvu produktu a ceny za jednotku.

`EditItemTemplate` lze vytvořit buď deklarativně, nebo prostřednictvím návrháře (výběrem možnosti Upravit šablony z inteligentní značky DataList s). Chcete-li použít možnost Upravit šablony, nejprve v inteligentní značce klikněte na odkaz Upravit šablony a v rozevíracím seznamu vyberte položku `EditItemTemplate`.

[![se přihlásit k rozhraní DataList s EditItemTemplate](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image19.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image18.png)

**Obrázek 8**: možnost pracovat s `EditItemTemplate` DataList ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image20.png))

Dále zadejte název produktu: a cena: a přetáhněte dva ovládací prvky TextBox ze sady nástrojů do rozhraní `EditItemTemplate` v návrháři. Nastavte textová pole `ID` vlastnosti na `ProductName` a `UnitPrice`.

[![přidat textové pole pro název produktu a cenu](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image22.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image21.png)

**Obrázek 9**: přidejte textové pole pro název produktu a cenu ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image23.png)

Musíme navazovat odpovídající hodnoty pole dat produktu na `Text` vlastnosti dvou textových polí. Z inteligentních značek TextBox klikněte na odkaz Upravit datové vazby a pak přidružte příslušné datové pole s vlastností `Text`, jak je znázorněno na obrázku 10.

> [!NOTE]
> Když svážete pole `UnitPrice` dat s polem `Text` TextBox s cenami, můžete ho naformátovat jako hodnotu měny (`{0:C}`), Obecné číslo (`{0:N}`) nebo nechat neformátovaný.

![Navažte datová pole NázevVýrobku a JednotkováCena na textové vlastnosti textových polí.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image24.png)

**Obrázek 10**: navázání datových polí `ProductName` a `UnitPrice` do vlastností `Text` pro textová pole

Všimněte si, jak dialogové okno Upravit datové vazby na obrázku 10 *nezahrnuje zaškrtávací* políčko pro oboustrannou vazbu, které je k dispozici při úpravách TemplateField v prvku GridView nebo DetailsView, nebo v šabloně ve třídě FormView. Funkce obousměrné datové vazby povoluje hodnotu zadanou do vstupního webového ovládacího prvku, která má být automaticky přiřazena k odpovídajícím `InsertParameters`ům ObjectDataSource s nebo `UpdateParameters` při vkládání nebo aktualizaci dat. DataList nepodporuje obousměrnou datovou vazbu, když se v tomto kurzu později dozvíte, po tom, co uživatel provede změny a je připraven k aktualizaci dat, budeme muset programově přistupovat k těmto textovým polím `Text` vlastnosti a předat jejich hodnoty příslušné `UpdateProduct` metodě ve třídě `ProductsBLL`.

Nakonec je potřeba přidat do `EditItemTemplate`tlačítka aktualizovat a zrušit. Jak jsme viděli v [hlavní a podrobné podobě pomocí seznamu hlavních záznamů s odrážkami v kurzu Details DataList](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) , když je na tlačítku, LinkButton nebo obrázkové, jehož vlastnost `CommandName` nastavena, kliknete na tlačítko Opakovat nebo DataList, vyvolá se událost Repeater nebo datalist s `ItemCommand`. V případě prvku DataList, pokud je vlastnost `CommandName` nastavena na určitou hodnotu, může být vyvolána i další událost. Mezi speciální `CommandName` hodnoty vlastností patří mimo jiné:

- Zrušit vyvolá událost `CancelCommand`.
- Upravit vyvolá událost `EditCommand`.
- Aktualizace vyvolá událost `UpdateCommand`.

Pamatujte, že tyto události jsou vyvolány *kromě* události `ItemCommand`.

Přidejte do `EditItemTemplate` dva webové ovládací prvky tlačítka, jejichž `CommandName` je nastavená na aktualizovat a druhá s nastaví na zrušit. Po přidání těchto dvou webových ovládacích prvků tlačítka by měl Návrhář vypadat podobně jako následující:

[![přidat do EditItemTemplate tlačítka aktualizovat a zrušit](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image26.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image25.png)

**Obrázek 11**: Přidání tlačítek aktualizovat a zrušit do `EditItemTemplate` ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image27.png))

`EditItemTemplate` dokončení deklarativních značek prvku DataList by měl vypadat nějak takto:

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample3.aspx)]

## <a name="step-5-adding-the-plumbing-to-enter-edit-mode"></a>Krok 5: Přidání domovní instalace pro přechod do režimu úprav

V tomto okamžiku má naše DataList rozhraní pro úpravy definované prostřednictvím jeho `EditItemTemplate`; Teď ale neexistuje žádný způsob, jak uživateli navštívit naši stránku, aby označoval, že chce upravit informace o produktu. Pro každý produkt musíme přidat tlačítko pro úpravy, které po kliknutí vykreslí tuto položku prvku DataList v režimu úprav. Začněte přidáním tlačítka pro úpravy do `ItemTemplate`, a to buď prostřednictvím návrháře, nebo deklarativně. Ujistěte se, že jste nastavili vlastnost upravit tlačítko `CommandName` na hodnotu upravit.

Po přidání tohoto tlačítka pro úpravy chvíli počkejte, než se stránka zobrazí v prohlížeči. V takovém případě by každý seznam produktů měl obsahovat tlačítko pro úpravy.

[![přidat do EditItemTemplate tlačítka aktualizovat a zrušit](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image29.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image28.png)

**Obrázek 12**: Přidání tlačítek aktualizovat a zrušit do `EditItemTemplate` ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image30.png))

Kliknutí na tlačítko způsobí postback, ale *nenačte seznam* produktů do režimu úprav. Aby bylo možné produkt upravovat, musíme:

1. Nastavte [vlastnost`EditItemIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) prvku DataList na index `DataListItem`, na které se právě kliknulo tlačítko pro úpravy.
2. Znovu Navažte data na prvek DataList. Když je prvek DataList znovu vykreslen, `DataListItem`, jehož `ItemIndex` odpovídá prvku DataList s `EditItemIndex`, se vykreslí pomocí jeho `EditItemTemplate`.

Vzhledem k tomu, že událost DataList `EditCommand` je aktivována při kliknutí na tlačítko pro úpravy, vytvořte obslužnou rutinu události `EditCommand` s následujícím kódem:

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample4.cs)]

Obslužná rutina události `EditCommand` je předána do objektu typu `DataListCommandEventArgs` jako druhý vstupní parametr, který obsahuje odkaz na `DataListItem` jejichž tlačítko Upravit bylo kliknuto (`e.Item`). Obslužná rutina události nejprve nastaví `EditItemIndex` prvku DataList na `ItemIndex` upravitelných `DataListItem` a poté znovu vytvoří vazby dat do prvku DataList voláním metody DataList s `DataBind()`.

Po přidání této obslužné rutiny události znovu navštivte stránku v prohlížeči. Kliknutím na tlačítko Upravit teď můžete kliknout na editovatelné produkt (viz obrázek 13).

[![kliknutí na tlačítko Upravit změní produkt na upravitelný](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image32.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image31.png)

**Obrázek 13**: kliknutím na tlačítko Upravit zpřístupníte produkt úpravou ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image33.png)).

## <a name="step-6-saving-the-user-s-changes"></a>Krok 6: uložení změn uživatelů

Kliknutím na upravená tlačítka pro aktualizaci produktů nebo zrušit v tuto chvíli nic neuděláte. pro přidání této funkce potřebujeme vytvořit obslužné rutiny událostí pro `UpdateCommand` a `CancelCommand` události DataList. Začněte vytvořením obslužné rutiny události `CancelCommand`, která se spustí, když se klikne na tlačítko pro zrušení upraveného produktu, které se zobrazí, a vrátí prvek DataList do jeho stavu před úpravou.

Chcete-li, aby prvek DataList vykreslil všechny položky v režimu jen pro čtení, musíme:

1. Nastavte [vlastnost`EditItemIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) prvku DataList na index neexistujícího `DataListItem` indexu. `-1` je bezpečná volba, protože `DataListItem` indexy začínají na `0`.
2. Znovu Navažte data na prvek DataList. Vzhledem k tomu, že žádné `DataListItem` `ItemIndex` ES neodpovídají `EditItemIndex`prvku DataList s, bude celá vlastnost DataList vykreslena v režimu jen pro čtení.

Tyto kroky lze provést s následujícím kódem obslužné rutiny události:

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample5.cs)]

S tímto přidáním kliknutím na tlačítko Storno vrátí prvek DataList do jeho stavu před úpravou.

Poslední obslužná rutina události, kterou je potřeba dokončit, je obslužná rutina `UpdateCommand` události. Tato obslužná rutina události musí:

1. Program programově přistupuje k názvu a ceně produktu zadaného uživatelem a také k upravovanému `ProductID`produktů.
2. Zahajte proces aktualizace voláním odpovídajícího `UpdateProduct` přetížení ve třídě `ProductsBLL`.
3. Nastavte [vlastnost`EditItemIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) prvku DataList na index neexistujícího `DataListItem` indexu. `-1` je bezpečná volba, protože `DataListItem` indexy začínají na `0`.
4. Znovu Navažte data na prvek DataList. Vzhledem k tomu, že žádné `DataListItem` `ItemIndex` ES neodpovídají `EditItemIndex`prvku DataList s, bude celá vlastnost DataList vykreslena v režimu jen pro čtení.

Kroky 1 a 2 jsou zodpovědné za uložení změn uživatelů. kroky 3 a 4 vrátí prvek DataList do stavu před úpravou poté, co byly změny uloženy a jsou stejné jako u kroků provedených v obslužné rutině `CancelCommand` události.

Abychom získali aktualizovaný název produktu a cenu, musíme použít metodu `FindControl` pro programové odkazování na webové ovládací prvky TextBox v rámci `EditItemTemplate`. Také je potřeba získat upravenou hodnotu `ProductID` produktů. Když zpočátku navážeme prvek ObjectDataSource k prvku DataList, Visual Studio přiřadilo vlastnost DataList s `DataKeyField` k hodnotě primárního klíče ze zdroje dat (`ProductID`). Tato hodnota se pak dá načíst z kolekce `DataKeys` DataList s. Chvíli zajistěte, aby byla vlastnost `DataKeyField` ve skutečnosti nastavená na hodnotu `ProductID`.

Následující kód implementuje čtyři kroky:

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample6.cs)]

Obslužná rutina události se spustí načtením z upravovaného `ProductID` produktů z kolekce `DataKeys`. Dále jsou odkazována dvě textová pole v `EditItemTemplate` a jejich `Text` vlastnosti uložené v místních proměnných, `productNameValue` a `unitPriceValue`. K načtení hodnoty z textového pole `UnitPrice` používáme metodu `Decimal.Parse()`, takže pokud zadaná hodnota má symbol měny, lze ji přesto správně převést na hodnotu `Decimal`.

> [!NOTE]
> Hodnoty z textových polí `ProductName` a `UnitPrice` jsou přiřazeny pouze k proměnným productNameValue a unitPriceValue, jsou-li vlastnosti textu TextBox zadány na hodnotu. V opačném případě se pro proměnné používá hodnota `Nothing`, která má vliv na aktualizaci dat pomocí databázové `NULL` hodnoty. To znamená, že náš kód zpracovává převod prázdných řetězců na hodnoty `NULL` databáze, což je výchozí chování rozhraní pro úpravy v ovládacích prvcích GridView, DetailsView a FormView.

Po přečtení hodnot je volána metoda `ProductsBLL` třídy s `UpdateProduct`, která předává název produktu, cenu a `ProductID`. Obslužná rutina události se dokončí vrácením prvku DataList do stavu před úpravou pomocí přesně stejné logiky jako v obslužné rutině události `CancelCommand`.

Po dokončení obslužných rutin událostí `EditCommand`, `CancelCommand`a `UpdateCommand` může návštěvník upravit název a cenu produktu. Obrázky 14-16 zobrazit tento pracovní postup úpravy v akci.

[![při první návštěvě stránky jsou všechny produkty v režimu jen pro čtení.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image35.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image34.png)

**Obrázek 14**: při první návštěvě stránky jsou všechny produkty v režimu jen pro čtení ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image36.png)

[![chcete aktualizovat název produktu nebo cenu, klikněte na tlačítko Upravit.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image38.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image37.png)

**Obrázek 15**: Chcete-li aktualizovat název produktu nebo cenu, klikněte na tlačítko Upravit ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image39.png)

[![po změně hodnoty klikněte na aktualizovat a vraťte se do režimu jen pro čtení.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image41.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image40.png)

**Obrázek 16**: po změně hodnoty klikněte na aktualizovat a vraťte se do režimu jen pro čtení ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image42.png)

## <a name="step-7-adding-delete-capabilities"></a>Krok 7: Přidání možností odstranění

Postup přidání možností odstranění do prvku DataList je podobný těm jako při přidávání možností úprav. V krátkém případě je potřeba přidat tlačítko Odstranit do `ItemTemplate`, když kliknete na:

1. Přečte v odpovídajících produktech `ProductID` prostřednictvím kolekce `DataKeys`.
2. Provede odstranění voláním metody `ProductsBLL` třídy s `DeleteProduct`.
3. Znovu naváže data na prvek DataList.

Nechte začít tím, že do `ItemTemplate`přidáte tlačítko pro odstranění.

Po kliknutí na tlačítko, jehož `CommandName` je upravit, aktualizovat nebo zrušit, dojde k události `ItemCommand` prvku DataList spolu s další událostí (například při použití úpravy události `EditCommand` je aktivována také). Podobně, jakékoli tlačítko, LinkButton nebo obrázkové v prvku DataList, jehož vlastnost `CommandName` je nastavena na hodnotu odstranit, způsobí, že se událost `DeleteCommand` vyvolá (společně s `ItemCommand`).

Přidejte tlačítko Odstranit vedle tlačítka upravit v `ItemTemplate`a nastavte jeho vlastnost `CommandName` na hodnotu odstranit. Po přidání tohoto ovládacího prvku tlačítko by vaše deklarativní syntaxe `ItemTemplate` DataList měla vypadat takto:

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample7.aspx)]

Dále vytvořte obslužnou rutinu události pro událost `DeleteCommand` DataList s použitím následujícího kódu:

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample8.cs)]

Kliknutím na tlačítko Odstranit dojde k postbacku a aktivuje se událost `DeleteCommand` DataList s. V obslužné rutině události se kliknutím na hodnotu `ProductID` produktů přistupuje z kolekce `DataKeys`. Dále se produkt odstraní voláním metody `ProductsBLL` třídy s `DeleteProduct`.

Po odstranění produktu je důležité, abyste data znovu navázali do prvku DataList (`DataList1.DataBind()`), jinak bude prvek DataList nadále zobrazovat produkt, který byl právě odstraněn.

## <a name="summary"></a>Souhrn

I když v prvku DataList chybí bod a klikne na možnost upravit a odstranit podporu, která je k dispozici v prvku GridView, s krátkým bitem kódu, může být vylepšena, aby obsahovala tyto funkce. V tomto kurzu jsme viděli, jak vytvořit seznam produktů se dvěma sloupci, které by se daly odstranit, a jejíž název a cenu by se daly upravit. Přidání podpory úprav a odstranění je záležitostí, která zahrnuje vhodné webové ovládací prvky v `ItemTemplate` a `EditItemTemplate`, vytváření odpovídajících obslužných rutin událostí, čtení hodnot zadaných uživatelem a primární klíč a propojení s vrstvou obchodní logiky.

Přidali jsme do prvku DataList základní možnosti pro úpravy a odstranění, ale chybí pokročilejší funkce. Například neexistují žádné ověření vstupního pole – Pokud uživatel zadá cenu za moc nákladný, vyvolá se při pokusu o převod příliš nákladného převodu do `Decimal`výjimka `Decimal.Parse`. Podobně pokud dojde k potížím při aktualizaci dat v obchodní Logic nebo vrstvách přístupu k datům, zobrazí se uživateli standardní chybová obrazovka. Bez jakéhokoli potvrzení na tlačítku odstranit je neúmyslně odstranit produkt, který je příliš pravděpodobný.

V budoucích kurzech se dozvíte, jak vylepšit uživatelské prostředí pro úpravy.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Zack Novotný, Ken Pespisa a Randy Schmidt. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](performing-batch-updates-cs.md)

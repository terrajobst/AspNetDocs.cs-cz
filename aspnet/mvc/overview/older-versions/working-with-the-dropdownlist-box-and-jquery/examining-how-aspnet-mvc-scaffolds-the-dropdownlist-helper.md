---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: Zkoumání toho, jak se ASP.NET (generování uživatelského rozhraní MVC) Pomocník pro DropDownList | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457606"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a>Zkoumání, jak ASP.NET MVC vygeneruje uživatelské rozhraní pomocné rutiny DropDownList

od [Rick Anderson](https://twitter.com/RickAndMSFT)

V **Průzkumník řešení**klikněte pravým tlačítkem na složku *Controllers* a pak vyberte **Přidat kontroler**. Pojmenujte kontroler **StoreManagerController**. V dialogovém okně **Přidat řadič** nastavte možnosti, jak je znázorněno na obrázku níže.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

Upravte zobrazení *StoreManager\Index.cshtml* a odeberte `AlbumArtUrl`. Po odebrání `AlbumArtUrl` bude prezentace čitelnější. Dokončený kód je uveden níže.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

Otevřete soubor *Controllers\StoreManagerController.cs* a vyhledejte metodu `Index`. Přidejte klauzuli `OrderBy`, aby se alba seřadila podle ceny. Úplný kód je uveden níže.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

Třídění podle ceny usnadňuje testování změn v databázi. Při testování metod Edit a Create můžete použít nízkou cenu, aby se uložená data zobrazovala jako první.

Otevřete soubor *StoreManager\Edit.cshtml* . Přidejte následující řádek hned za značku legendy.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

Následující kód ukazuje kontext této změny:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

`AlbumId` je nutné provést změny v záznamu alba.

Stiskněte klávesy CTRL+F5 a spusťte aplikaci. Vyberte odkaz pro **správce** a pak výběrem odkazu **vytvořit nový** vytvořte nové album. Ověřte, že informace o albu byly uloženy. Upravte album a ověřte, že změny, které jste provedli, jsou trvalé.

### <a name="the-album-schema"></a>Schéma alba

Kontroler `StoreManager` vytvořený mechanismem generování uživatelského rozhraní MVC umožňuje CRUD (vytvořit, číst, aktualizovat, odstranit) přístup k albu v databázi úložiště hudby. Schéma pro informace o albu se zobrazuje níže:

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

Tabulka `Albums` neukládá Žánr a popis alba, ukládá do tabulky `Genres` cizí klíč. Tabulka `Genres` obsahuje název a popis žánru. Podobně `Albums` tabulka neobsahuje název umělců alba, ale cizí klíč do tabulky `Artists`. Tabulka `Artists` obsahuje jméno umělce. Pokud prohlížíte data v tabulce `Albums`, vidíte každý řádek obsahuje cizí klíč do tabulky `Genres` a cizí klíč do tabulky `Artists`. Následující obrázek ukazuje data tabulky z `Albums` tabulky.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a>Značka výběru HTML

Element HTML `<select>` (vytvořený pomocí pomocníka [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) HTML) slouží k zobrazení úplného seznamu hodnot (například seznamu žánrů). Pro upravit formuláře, pokud je aktuální hodnota známa, může seznam SELECT zobrazit aktuální hodnotu. Tuto možnost jsme dřív viděli, když jsme tuto hodnotu nastavili na **komedie**. Seznam pro výběr je ideální pro zobrazení dat kategorie nebo cizího klíče. Element `<select>` pro cizí klíč žánru zobrazuje seznam možných názvů žánrů, ale při uložení formuláře se vlastnost Žánr aktualizuje s hodnotou cizího klíče žánru, nikoli zobrazeným názvem žánru. Na následujícím obrázku je vybraný Žánr na **discích** a interpret je **Donnou letního**.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a>Zkoumání generovaného kódu ASP.NET MVC

Otevřete soubor *Controllers\StoreManagerController.cs* a vyhledejte metodu `HTTP GET Create`.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

Metoda `Create` přidá do `ViewBag`dva objekty [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) , jeden, který obsahuje informace o žánru, a druhý, který obsahuje informace o interpretu. Výše použité přetížení konstruktoru [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) má tři argumenty:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. *Items*: rozhraní [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) obsahující položky v seznamu. V předchozím příkladu je uveden seznam žánrů vrácených `db.Genres`.
2. *dataValueField*: název vlastnosti v seznamu **IEnumerable** , který obsahuje hodnotu klíče. V předchozím příkladu `GenreId` a `ArtistId`.
3. *dataTextField*: název vlastnosti v seznamu **IEnumerable** obsahující informace, které se mají zobrazit. V tabulce interpreti a žánru se používá pole `name`.

Otevřete soubor *Views\StoreManager\Create.cshtml* a Projděte si označení pomocné rutiny `Html.DropDownList` pro pole Žánr.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

První řádek ukazuje, že zobrazení vytvořit přebírá model `Album`. Ve výše uvedené metodě `Create` nebyl předán žádný model, takže zobrazení získá `Album` model s **hodnotou null** . V tuto chvíli vytváříme nové album, takže pro něj neexistují žádná `Album` data.

Výše zobrazené přetížení [HTML. DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) vezme název pole, které se má vytvořit jako vazby k modelu. Tento název také používá k vyhledání objektu **ViewBag** obsahujícího objekt [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) . Pomocí tohoto přetížení budete muset pojmenovat objekt **ViewBag SelectList** `GenreId`. Druhý parametr (`String.Empty`) je text, který se zobrazí, když není vybrána žádná položka. To je přesně to, co chceme při vytváření nového alba. Pokud jste odebrali druhý parametr a použili jste následující kód:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

Seznam SELECT by byl výchozím nastavením prvního prvku nebo rock v naší ukázce.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

Prověřování metody `HTTP POST Create`.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

Toto přetížení metody `Create` přebírá objekt `album` vytvořený systémem vazeb modelu ASP.NET MVC z publikovaných hodnot formuláře. Pokud odešlete nové album, pokud je stav modelu platný a nejsou k dispozici žádné chyby databáze, přidá se k novému albu databáze. Následující obrázek ukazuje vytvoření nového alba.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

Pomocí [nástroje Fiddler](http://www.fiddler2.com/fiddler2/) můžete prostudovat zaúčtované hodnoty formulářů, které ASP.NET MVC modelů používá k vytvoření objektu alba.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).

### <a name="refactoring-the-viewbag-selectlist-creation"></a>Refaktoring SelectList vytváření ViewBag

Metody `Edit` a metoda `HTTP POST Create` mají stejný kód pro nastavení **SelectList** v **ViewBag**. V duchu [suchého](http://en.wikipedia.org/wiki/Don't_repeat_yourself)kódu budeme tento kód Refaktorovat. Pomocí tohoto refaktoringového kódu ho později využijeme.

Vytvořte novou metodu pro přidání žánru a interpreta **SelectList** do **ViewBag**.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

Nahraďte dva řádky nastavením `ViewBag` v každé z `Create` a `Edit` metody voláním metody `SetGenreArtistViewBag`. Dokončený kód je uveden níže.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

Vytvořením nového alba a úpravou alba ověřte, zda změny fungují.

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a>Explicitní předání SelectList do DropDownList

Zobrazení vytvořit a upravit vytvořená pomocí generování uživatelského rozhraní ASP.NET MVC používají následující přetížení **DropDownList** :

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

`DropDownList` značky pro zobrazení pro vytváření jsou uvedeny níže.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

Vzhledem k tomu, že vlastnost `ViewBag` pro `SelectList` má název `GenreId`, pomocník **DropDownList** použije `GenreId`**SelectList** v **ViewBag**. V následujícím přetížení **DropDownList** je `SelectList` explicitně předán v.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

Otevřete soubor *Views\StoreManager\Edit.cshtml* a změňte volání **DropDownList** tak, aby explicitně předávalo v **SelectList**, pomocí výše uvedeného přetížení. Proveďte tuto kategorii žánru. Dokončený kód je zobrazen níže:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

Spusťte aplikaci a klikněte na odkaz **správce** , přejděte na album jazz a vyberte odkaz **Upravit** .

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

Místo zobrazení Jazz jako aktuálně vybraného žánru se zobrazí rock. Pokud má argument řetězce (vlastnost k vytvoření vazby) a objekt **SelectList** stejný název, vybraná hodnota se nepoužije. Pokud není zadána žádná vybraná hodnota, prohlížeče se standardně naplní na první prvek v **SelectList**(což je **Rock** v příkladu výše). Toto je známé omezení pomocné rutiny **DropDownList** .

Otevřete soubor *Controllers\StoreManagerController.cs* a změňte názvy objektů **SelectList** na `Genres` a `Artists`. Dokončený kód je zobrazen níže:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

Názvy žánrů a umělců mají lepší názvy kategorií, protože obsahují více než pouze ID každé kategorie. Refaktoring, kterou jsme dříve vyplatili. Místo změny **ViewBag** ve čtyřech metodách byly tyto změny izolovány na metodu `SetGenreArtistViewBag`.

Chcete-li použít nové názvy **SelectList** , změňte volání **DropDownList** v zobrazeních Create a Edit. Nové značky pro zobrazení pro úpravy jsou uvedené níže:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

Zobrazení vytvořit vyžaduje prázdný řetězec, aby se zabránilo zobrazení první položky v SelectList.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

Vytvořením nového alba a úpravou alba ověřte, zda změny fungují. Otestujte kód úprav tak, že vyberete album s jiným žánrem než rock.

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a>Použití modelu zobrazení s pomocníkem DropDownList

Vytvořte novou třídu ve složce ViewModels s názvem `AlbumSelectListViewModel`. Nahraďte kód ve třídě `AlbumSelectListViewModel` následujícím kódem:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

Konstruktor `AlbumSelectListViewModel` převezme album, Seznam umělců a žánrů a vytvoří objekt obsahující album a `SelectList` pro žánry a interprety.

Sestavte projekt, aby `AlbumSelectListViewModel` k dispozici, když vytvoříme zobrazení v dalším kroku.

Přidejte do `StoreManagerController`metodu `EditVM`. Dokončený kód je uveden níže.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

Klikněte pravým tlačítkem `AlbumSelectListViewModel`, vyberte **vyřešit**a pak **použijte MvcMusicStore. ViewModels;** .

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

Alternativně můžete přidat následující příkaz using:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

Klikněte pravým tlačítkem `EditVM` a vyberte **Přidat zobrazení**. Použijte níže uvedené možnosti.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

Vyberte **Přidat**a potom nahraďte obsah souboru *Views\StoreManager\EditVM.cshtml* následujícím způsobem:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

Kód `EditVM` se velmi podobá původnímu `Edit` označení pomocí následujících výjimek.

- Vlastnosti modelu v zobrazení `Edit` mají `model.property`formuláře (například `model.Title`). Vlastnosti modelu v zobrazení `EditVm` mají `model.Album.property`formuláře (například `model.Album.Title`). Důvodem je, že zobrazení `EditVM` předává kontejner pro `Album`, nikoli `Album` jako v `Edit`ém zobrazení.
- Druhý parametr **DropDownList** pochází z modelu zobrazení, ne z **ViewBag**.
- Pomocná rutina **BeginForm** v zobrazení `EditVM` explicitně odesílá zpět do metody `Edit` akce. Po odeslání zpět do akce `Edit` nemusíme psát `HTTP POST EditVM` akci a může znovu použít `HTTP POST` `Edit` akci.

Spusťte aplikaci a upravte album. Změňte adresu URL na použití `EditVM`. Změňte pole a stiskněte tlačítko **Uložit** a ověřte, zda kód funguje.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a>Který přístup byste měli použít?

Všechny uvedené tři přístupy jsou přijatelné. Mnoho vývojářů upřednostňuje explicitně předat `SelectList` do `DropDownList` pomocí `ViewBag`. Tento přístup má výhodu k tomu, abyste vám poskytli flexibilitu při používání vhodnějšího názvu kolekce. Jediným aspektem je, že objekt `ViewBag SelectList` nemůžete pojmenovat stejným názvem jako vlastnost modelu.

Někteří vývojáři upřednostňují přístup k ViewModel. Jiné považují podrobnější značky a vygenerovaný kód HTML ViewModel přístupu k nevýhodám.

V této části jsme zjistili tři přístupy k použití ovládacího prvkem **DropDownList** s daty kategorií. V další části si ukážeme, jak přidat novou kategorii.

> [!div class="step-by-step"]
> [Předchozí](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [Další](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)

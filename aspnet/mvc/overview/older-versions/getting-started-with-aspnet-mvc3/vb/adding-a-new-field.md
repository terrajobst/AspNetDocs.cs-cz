---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
title: Přidání nového pole do modelu a tabulky databáze (VB) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 28970e1b-1845-4015-86ef-121e52a6c397
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: b2b26b6009c55f02c8a4159bda839fe7aefea4c0
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457259"
---
# <a name="adding-a-new-field-to-the-movie-model-and-database-table-vb"></a>Přidání nového pole do modelu a databázové tabulky Movie (VB)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:
> 
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)
> 
> Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt Visual Web Developer s VB.NET zdrojovým kódem je k dispozici pro toto téma. [Stáhněte si verzi VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost C#, přepněte se na [ C# verzi](../cs/adding-a-new-field.md) tohoto kurzu.

V této části provedete některé změny tříd modelu a zjistíte, jak můžete aktualizovat schéma databáze tak, aby odpovídalo změnám modelu.

## <a name="adding-a-rating-property-to-the-movie-model"></a>Přidání vlastnosti hodnocení do modelu videa

Začněte přidáním nové vlastnosti `Rating` do existující třídy `Movie`. Otevřete soubor *Movie.cs* a přidejte vlastnost `Rating`, jako je tato:

[!code-vb[Main](adding-a-new-field/samples/sample1.vb)]

Úplná `Movie` třída teď vypadá jako v následujícím kódu:

[!code-vb[Main](adding-a-new-field/samples/sample2.vb)]

Znovu zkompilujte aplikaci pomocí příkazu **Debug** &gt;**Build Movie** nabídky.

Teď, když jste aktualizovali `Model` třídu, budete také muset aktualizovat šablony zobrazení *\Views\Movies\Index.vbhtml* a *\Views\Movies\Create.vbhtml* , aby se podporovala nová vlastnost `Rating`.

Otevřete soubor<em>\Views\Movies\Index.vbhtml</em> a přidejte `<th>Rating</th>` záhlaví sloupce hned za sloupec <strong>Price</strong> . Pak přidejte `<td>` sloupec poblíž konce šablony, aby se vygenerovala `@item.Rating` hodnota. Níže je uveden aktualizovaný vzhled šablony zobrazení <em>index. vbhtml</em> jako:

[!code-vbhtml[Main](adding-a-new-field/samples/sample3.vbhtml)]

Potom otevřete soubor *\Views\Movies\Create.vbhtml* a přidejte následující kód poblíž konce formuláře. Tím vykreslíte textové pole, abyste mohli při vytváření nového filmu zadat hodnocení.

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a>Správa rozdílů v modelu a schématu databáze

Nyní jste aktualizovali kód aplikace, aby podporoval novou vlastnost `Rating`.

Nyní spusťte aplikaci a přejděte na adresu URL */Movies* . Když to uděláte, zobrazí se tato chyba:

![](adding-a-new-field/_static/image1.png)

Tato chyba se zobrazuje, protože aktualizovaná třída modelu `Movie` v aplikaci je nyní odlišná od schématu `Movie` tabulky existující databáze. (V tabulce databáze nejsou žádné `Rating` sloupce.)

Ve výchozím nastavení platí, že při použití Entity Framework Code First k automatickému vytvoření databáze, stejně jako v tomto kurzu, Code First přidá do databáze tabulku, která bude sledovat, zda je schéma databáze synchronizované s třídami modelů, ze kterých byla vygenerována. Pokud nejsou synchronizované, Entity Framework vyvolá chybu. Díky tomu je snazší sledovat problémy v době vývoje, které byste jinak mohli najít (překrytím chyb) v době běhu. Funkce synchronizace se ověřuje tím, že se zobrazí chybová zpráva, kterou jste právě viděli.

Existují dva přístupy k řešení této chyby:

1. Entity Framework automaticky vyřadit a znovu vytvořit databázi na základě nového schématu třídy modelu. Tento přístup je velmi výhodný při aktivním vývoji na testovací databázi, protože umožňuje rychlou vývoj modelu a schématu databáze dohromady. Nevýhodou, ale je to, že ztratíte stávající data v databázi, takže *nechcete tento* přístup použít v provozní databázi.
2. Explicitně upravte schéma existující databáze tak, aby odpovídalo třídám modelu. Výhodou tohoto přístupu je, že zachováte data. Tuto změnu můžete provést buď ručně, nebo vytvořením skriptu změny databáze.

V tomto kurzu použijeme první přístup – budete mít Entity Framework Code First automaticky znovu vytvořit databázi, kdykoli se změní model.

## <a name="automatically-re-creating-the-database-on-model-changes"></a>Automatické opětovné vytvoření databáze při změnách modelu

Pojďme aplikaci aktualizovat tak, aby Code First automaticky vynechala a znovu vytvořila databázi, kdykoli změníte model aplikace.

> [!NOTE] 
> 
> **Upozornění** Tento postup je vhodné povolit pro automatické vyřazení a opětovné vytvoření databáze pouze v případě, že používáte vývojové nebo testovací databáze a *nikdy* nemáte v provozní databázi, která obsahuje skutečná data. Použití na provozním serveru může způsobit ztrátu dat.

V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a pak vyberte **Třída**.

![](adding-a-new-field/_static/image2.png)

Pojmenujte třídu &quot;MovieInitializer&quot;. Aktualizujte třídu `MovieInitializer` tak, aby obsahovala následující kód:

[!code-vb[Main](adding-a-new-field/samples/sample5.vb)]

Třída `MovieInitializer` určuje, že databáze používaná modelem by měla být vyřazena a automaticky vytvořena, pokud se třídy modelů stále mění. Kód obsahuje metodu `Seed` k určení některých výchozích dat, která mají být automaticky přidána do databáze při každém vytvoření (nebo opětovném vytvoření). To poskytuje užitečný způsob, jak naplnit databázi pomocí některých ukázkových dat, aniž byste je museli ručně naplnit pokaždé, když provedete změnu modelu.

Teď, když jste definovali `MovieInitializer` třídu, budete ji chtít nasměrovat tak, aby pokaždé, když se aplikace spustí, zkontroluje, jestli se třídy modelu liší od schématu v databázi. Pokud jsou, můžete spustit inicializátor pro opětovné vytvoření databáze, aby odpovídala modelu, a pak naplnit databázi ukázkovými daty.

Otevřete soubor *Global. asax* , který je v kořenovém adresáři projektu `MvcMovies`:

Soubor *Global. asax* obsahuje třídu, která definuje celou aplikaci pro projekt, a obsahuje `Application_Start` obslužnou rutinu události, která se spouští při prvním spuštění aplikace.

Vyhledejte metodu `Application_Start` a přidejte volání `Database.SetInitializer` na začátku metody, jak je znázorněno níže:

[!code-vb[Main](adding-a-new-field/samples/sample6.vb)]

Příkaz `Database.SetInitializer`, který jste právě přidali, indikuje, že databáze používaná instancí `MovieDBContext` by měla být automaticky odstraněna a znovu vytvořena, pokud se schéma a databáze neshodují. A jak jste viděli, naplní databázi také ukázkovými daty, která jsou zadána ve třídě `MovieInitializer`.

Zavřete soubor *Global. asax* .

Spusťte aplikaci znovu a přejděte na adresu URL */Movies* . Po spuštění aplikace zjistí, že struktura modelu již neodpovídá schématu databáze. Automaticky znovu vytvoří databázi tak, aby odpovídala nové struktuře modelů a naplnila databázi ukázkovými filmy:

![7_MyMovieList_SM](adding-a-new-field/_static/image3.png)

Kliknutím na odkaz **vytvořit nový** přidejte nový film. Všimněte si, že můžete přidat hodnocení.

[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)

Klikněte na možnost **Vytvořit**. Nový film, včetně hodnocení, se teď zobrazí v seznamu filmů:

![7_ourNewMovie_SM](adding-a-new-field/_static/image6.png)

V této části jste viděli, jak můžete upravovat objekty modelu a udržovat databázi synchronizované se změnami. Zjistili jste taky způsob, jak naplnit nově vytvořenou databázi pomocí ukázkových dat, abyste si mohli vyzkoušet scénáře. Teď se podíváme na to, jak můžete přidat bohatou logiku ověřování do tříd modelu a povolit uplatnění některých obchodních pravidel.

> [!div class="step-by-step"]
> [Předchozí](examining-the-edit-methods-and-edit-view.md)
> [Další](adding-validation-to-the-model.md)

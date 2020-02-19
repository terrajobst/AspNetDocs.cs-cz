---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-validation-to-the-model
title: Přidání ověření do modelu (VB) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 878f6c31-972d-45f4-8849-5c633b511409
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 7f3f195bc30ed23a637b59f15e6fc8431e39e217
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457194"
---
# <a name="adding-validation-to-the-model-vb"></a>Přidání ověření do modelu (VB)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:
> 
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)
> 
> Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt Visual Web Developer s VB.NET zdrojovým kódem je k dispozici pro toto téma. [Stáhněte si verzi VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost C#, přepněte se na [ C# verzi](../cs/adding-validation-to-the-model.md) tohoto kurzu.

V této části přidáte logiku ověřování do modelu `Movie` a zajistěte, aby se ověřovací pravidla vynutila pokaždé, když se uživatel pokusí vytvořit nebo upravit film pomocí aplikace.

## <a name="keeping-things-dry"></a>Udržování věcí v SUŠINě

Jedna z hlavních principy návrhu ASP.NET MVC je SUCHá ("princip"Neopakuj se""). ASP.NET MVC vám doporučuje zadat funkce nebo chování jenom jednou a pak je nechat odrážet všude v aplikaci. Tím se sníží množství kódu, který musíte napsat, a kód, který zapíšete, je mnohem snazší.

Podpora ověřování poskytovaná ASP.NET MVC a Entity Framework Code First je skvělým příkladem SUCHÉho principu v akci. Můžete deklarativně zadat pravidla ověřování na jednom místě (ve třídě modelu) a pak jsou tato pravidla vynutila všude v aplikaci.

Pojďme se podívat, jak můžete využít tuto podporu ověřování v aplikaci Movie.

## <a name="adding-validation-rules-to-the-movie-model"></a>Přidání ověřovacích pravidel do modelu filmů

Začnete přidáním nějaké ověřovací logiky do třídy `Movie`.

Otevřete soubor *Movie. vb* . Přidejte do horní části souboru příkaz `Imports`, který odkazuje na obor názvů [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) :

[!code-vb[Main](adding-validation-to-the-model/samples/sample1.vb)]

Obor názvů je součástí .NET Framework. Poskytuje vestavěnou sadu ověřovacích atributů, které lze deklarativně použít pro libovolnou třídu nebo vlastnost.

Teď aktualizujte třídu `Movie`, abyste mohli využívat předdefinované atributy ověřování [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)a [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) . Použijte následující kód jako příklad, kde použít atributy.

[!code-vb[Main](adding-validation-to-the-model/samples/sample2.vb)]

Atributy ověřování určují chování, které chcete vyhovět pro vlastnosti modelu, na které se aplikují. Atribut `Required` označuje, že vlastnost musí mít hodnotu. v této ukázce musí mít film hodnotu pro vlastnosti `Title`, `ReleaseDate`, `Genre`a `Price`, aby bylo možné je platné. Atribut `Range` omezuje hodnotu na v zadaném rozsahu. Atribut `StringLength` umožňuje nastavit maximální délku řetězcové vlastnosti a volitelně její minimální délku.

Code First zajistí, aby se ověřovací pravidla, která zadáte pro třídu modelu, vynutila předtím, než aplikace uloží změny v databázi. Například následující kód vyvolá výjimku při volání metody `SaveChanges`, protože chybí několik požadovaných `Movie` hodnot vlastností a cena je nulová (což je mimo platný rozsah).

[!code-vb[Main](adding-validation-to-the-model/samples/sample3.vb)]

Automatické vynucení ověřovacích pravidel .NET Framework pomáhá zajistit větší odolnost aplikace. Také zajišťuje, že se nebudete moci zapomenout a neúmyslně ověřit data v databázi.

Zde je kompletní výpis kódu pro aktualizovaný soubor *Movie. vb* :

[!code-vb[Main](adding-validation-to-the-model/samples/sample4.vb)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>Uživatelské rozhraní chyby ověřování v ASP.NET MVC

Spusťte aplikaci znovu a přejděte na adresu URL */Movies* .

Kliknutím na odkaz **vytvořit film** přidejte nový film. Vyplňte formulář s některými neplatnými hodnotami a pak klikněte na tlačítko **vytvořit** .

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

Všimněte si, jak formulář automaticky použil barvu pozadí k zvýraznění textových polí, která obsahují neplatná data a vygenerovala příslušné chybové zprávy ověření vedle každého z nich. Chybové zprávy odpovídají chybovým řetězcům, které jste zadali při zadání poznámky `Movie` třídy. Chyby se vynutily na straně klienta (pomocí JavaScriptu) a na straně serveru (Pokud uživatel má zakázaný JavaScript).

Reálnou výhodou je, že nemusíte změnit jeden řádek kódu ve třídě `MoviesController` nebo v zobrazení *vytvořit. vbhtml* , aby bylo možné toto uživatelské rozhraní pro ověřování povolit. Kontroler a zobrazení, které jste vytvořili dříve v tomto kurzu, automaticky vybrala ověřovací pravidla, která jste zadali pomocí atributů `Movie` třídy modelu.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Jak probíhá ověřování v metodě vytvořit zobrazení a vytvořit akci

Můžete se setkat s tím, jak se ověřovací uživatelské rozhraní vygenerovalo bez jakýchkoli aktualizací kódu v řadiči nebo zobrazeních. Následující výpis ukazuje, jak `Create` metody ve třídě `MovieController` vypadají jako. Nezměnili jste je, jak jste je vytvořili dříve v tomto kurzu.

[!code-vb[Main](adding-validation-to-the-model/samples/sample5.vb)]

První metoda Action zobrazí počáteční formulář pro vytvoření. Druhý zpracovává příspěvek formuláře. Druhá metoda `Create` volá `ModelState.IsValid`, aby zkontrolovala, jestli má film nějaké chyby ověřování. Volání této metody vyhodnotí všechny atributy ověřování, které byly aplikovány na objekt. Pokud objekt obsahuje chyby ověřování, metoda `Create` znovu zobrazí formulář. Pokud nejsou k dispozici žádné chyby, metoda uloží nový film do databáze.

Níže je uvedená šablona zobrazení *vytvořit. vbhtml* , kterou jste vystavili dříve v tomto kurzu. Používá metody akcí zobrazené výše k zobrazení počátečního formuláře a jeho zobrazení v případě chyby.

[!code-vbhtml[Main](adding-validation-to-the-model/samples/sample6.vbhtml)]

Všimněte si, jak kód používá pomoc `Html.EditorFor` k výstupu prvku `<input>` pro každou vlastnost `Movie`. Vedle této pomocné rutiny je volání pomocné metody `Html.ValidationMessageFor`. Tyto dvě pomocné metody fungují s objektem modelu, který je předán řadičem do zobrazení (v tomto případě objekt `Movie`). Automaticky hledají ověřovací atributy zadané v modelu a zobrazují chybové zprávy podle potřeby.

To je prakticky Skvělé o tomto přístupu, protože neví, že řadič ani šablona pro vytváření zobrazení neví žádné informace o skutečných ověřovacích pravidlech a o tom, jaké jsou zobrazené chybové zprávy. Ověřovací pravidla a řetězce chyb jsou určeny pouze ve třídě `Movie`.

Pokud chcete logiku ověřování později změnit, můžete to udělat přesně na jednom místě. Nemusíte se starat o různé části aplikace, které jsou nekonzistentní s tím, jak se pravidla uplatňují – veškerá logika ověřování bude definovaná na jednom místě a bude se používat všude. Tím se kód neustále čistí a usnadňuje se jeho údržba a vývoj. A to znamená, že budete plně dodržovat zásadu SUCHÉho.

## <a name="adding-formatting-to-the-movie-model"></a>Přidání formátování do modelu videa

Otevřete soubor *Movie. vb* . Obor názvů [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) poskytuje kromě předdefinované sady ověřovacích atributů také atributy formátování. Použijete atribut [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) a hodnotu výčtu [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) na datum vydání a pole s cenami. Následující kód ukazuje vlastnosti `ReleaseDate` a `Price` s odpovídajícím atributem [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) .

[!code-vb[Main](adding-validation-to-the-model/samples/sample7.vb)]

Případně můžete explicitně nastavit [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) hodnotu. Následující kód ukazuje vlastnost datum vydání s řetězcem formátu data (konkrétně "d"). Pomocí tohoto nastavení určíte, že jako součást data vydání nechcete čas.

[!code-vb[Main](adding-validation-to-the-model/samples/sample8.vb)]

Následující kód formátuje vlastnost `Price` jako měnu.

[!code-vb[Main](adding-validation-to-the-model/samples/sample9.vb)]

Kompletní `Movie` třída je uvedena níže.

[!code-vb[Main](adding-validation-to-the-model/samples/sample10.vb)]

Spusťte aplikaci a přejděte k řadiči `Movies`.

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

V další části série si probereme aplikaci a provedeme některá vylepšení automaticky generovaných `Details` a `Delete`ch metod.

> [!div class="step-by-step"]
> [Předchozí](adding-a-new-field.md)
> [Další](improving-the-details-and-delete-methods.md)

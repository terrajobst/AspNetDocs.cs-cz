---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: Ověřování pomocí rozhraní IDataErrorInfo (C#) | Microsoft Docs
author: StephenWalther
description: Stephen Walther ukazuje, jak zobrazit chybové zprávy vlastního ověřování implementací rozhraní IDataErrorInfo v třídě modelu.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 938b180da02b1963acffd021d18621d75d1d0447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542558"
---
# <a name="validating-with-the-idataerrorinfo-interface-c"></a>Ověřování v rozhraní IDataErrorInfo (C#)

od [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther ukazuje, jak zobrazit chybové zprávy vlastního ověřování implementací rozhraní IDataErrorInfo v třídě modelu.

Cílem tohoto kurzu je vysvětlit jeden přístup k provádění ověřování v aplikaci ASP.NET MVC. Naučíte se, jak zabránit odeslání formuláře HTML bez zadání hodnot pro požadovaná pole formuláře. V tomto kurzu se naučíte provádět ověřování pomocí rozhraní IErrorDataInfo.

## <a name="assumptions"></a>Předpoklady

V tomto kurzu použijeme databázi MoviesDB a databázovou tabulku filmů. Tato tabulka obsahuje následující sloupce:

<a id="0.5_table01"></a>

| **Název sloupce** | **Datový typ** | **Povoluje hodnoty null.** |
| --- | --- | --- |
| ID | Int | False |
| Název | Nvarchar(100) | False |
| Ředitel | Nvarchar(100) | False |
| DateReleased | DateTime | False |

V tomto kurzu použijeme Microsoft Entity Framework k vygenerování tříd databázového modelu. Třída Movie vygenerovaná Entity Framework je zobrazena na obrázku 1.

[![entitě video](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)

**Obrázek 01**: entita video ([kliknutím zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))

> [!NOTE] 
> 
> Další informace o použití Entity Framework k vygenerování tříd databázového modelu naleznete v tématu můj kurz s názvem vytváření tříd modelu pomocí Entity Framework.

## <a name="the-controller-class"></a>Třída Controller

K vypsání filmů a vytváření nových filmů používáme domovský kontroler. Kód pro tuto třídu je obsažen v seznamu 1.

**Výpis 1 – souboru controllers\homecontroller.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

Třída domovského kontroleru v seznamu 1 obsahuje dvě akce Create (). První akce zobrazí formulář HTML pro vytvoření nového filmu. Druhá akce Create () provede vlastní vložení nového videa do databáze. Druhá akce Create () je vyvolána, když je formulář zobrazený první akcí Create () na server.

Všimněte si, že druhá akce Create () obsahuje následující řádky kódu:

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

Vlastnost IsValid vrátí hodnotu false, pokud dojde k chybě ověřování. V takovém případě se zobrazí znovu zobrazení vytvořit, které obsahuje formulář HTML pro vytvoření filmu.

## <a name="creating-a-partial-class"></a>Vytvoření částečné třídy

Třída Movie je vygenerována Entity Framework. Pokud rozbalíte soubor MoviesDBModel. edmx v okně Průzkumník řešení a otevřete soubor MoviesDBModel.Designer.cs v editoru kódu (viz obrázek 2), můžete zobrazit kód pro třídu filmu.

[![kódu pro entitu video](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)

**Obrázek 02**: kód pro entitu video ([kliknutím zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))

Třída Movie je částečnou třídou. To znamená, že můžeme přidat další částečnou třídu se stejným názvem, aby bylo možné roztáhnout funkce třídy video. Do nové dílčí třídy přidáme naši logiku ověřování.

Přidejte třídu v seznamu 2 do složky modely.

**Výpis 2 – Models\Movie.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

Všimněte si, že třída v seznamu 2 obsahuje *částečný* modifikátor. Jakékoli metody nebo vlastnosti, které přidáte do této třídy, se stanou součástí třídy filmu vygenerované Entity Framework.

## <a name="adding-onchanging-and-onchanged-partial-methods"></a>Přidávají se částečné metody s jednou změnou a při změně.

Když Entity Framework generuje třídu entity, Entity Framework automaticky přidá částečné metody do třídy. Entity Framework generuje proměnlivé a přiměnitelné částečné metody, které odpovídají jednotlivým vlastnostem třídy.

V případě třídy video vytvoří Entity Framework následující metody:

- OnIdChanging
- OnIdChanged
- OnTitleChanging
- OnTitleChanged
- OnDirectorChanging
- OnDirectorChanged
- OnDateReleasedChanging
- OnDateReleasedChanged

Metoda při změně je volána přímo před změnou odpovídající vlastnosti. Metoda prochange je volána hned po změně vlastnosti.

Tyto částečné metody můžete využít k přidání logiky ověřování do třídy filmu. Třída aktualizační filmy v seznamu 3 ověřuje, že vlastnosti title a Director jsou přiřazeny neprázdné hodnoty.

> [!NOTE] 
> 
> Částečná metoda je metoda definovaná ve třídě, kterou není nutné implementovat. Pokud neimplementujete částečnou metodu, kompilátor odstraní signaturu metody a veškerá volání metody, takže neexistují žádné náklady za běhu spojené s částečnou metodou. V editoru Visual Studio Code můžete přidat částečnou metodu zadáním klíčového slova *Partial* následovaného mezerou pro zobrazení seznamu částečných implementací.

**Výpis 3 – Models\Movie.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

Například pokud se pokusíte k vlastnosti title přiřadit prázdný řetězec, chybová zpráva je přiřazena ke slovníku s názvem \_chyby.

V tuto chvíli se nic nestane, když přiřadíte prázdný řetězec k vlastnosti title a do pole chyby Private \_se přidá chyba. Abychom vystavili tyto chyby ověřování v architektuře ASP.NET MVC, musíme implementovat rozhraní IDataErrorInfo.

## <a name="implementing-the-idataerrorinfo-interface"></a>Implementace rozhraní IDataErrorInfo

Rozhraní IDataErrorInfo bylo součástí rozhraní .NET Framework od první verze. Toto rozhraní je velmi jednoduché rozhraní:

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

Pokud třída implementuje rozhraní IDataErrorInfo, rozhraní ASP.NET MVC bude toto rozhraní používat při vytváření instance třídy. Například akce domů kontroleru Create () přijímá instanci třídy video:

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

Rozhraní ASP.NET MVC vytvoří instanci filmu předanou akci Create () pomocí pořadače modelu (DefaultModelBinder). Pořadač modelů zodpovídá za vytvoření instance objektu filmu navázáním polí formuláře HTML na instanci objektu video.

DefaultModelBinder zjistí, zda třída implementuje rozhraní IDataErrorInfo. Pokud třída implementuje toto rozhraní, pořadač modelu vyvolá IDataErrorInfo. Tento indexer pro každou vlastnost třídy. Pokud indexer vrátí chybovou zprávu, přidá pořadač modelů tuto chybovou zprávu do stavu modelu automaticky.

DefaultModelBinder také kontroluje vlastnost IDataErrorInfo. Error. Tato vlastnost slouží k reprezentaci chyb ověřování specifických pro jiné než vlastnosti, které jsou přidruženy ke třídě. Můžete například vynutili ověřovací pravidlo, které závisí na hodnotách více vlastností třídy video. V takovém případě byste vrátili chybu ověřování z vlastnosti Error.

Aktualizovaná třída filmu v seznamu 4 implementuje rozhraní IDataErrorInfo.

**Výpis 4 – Models\Movie.cs (implementuje IDataErrorInfo)**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

V seznamu 4 vlastnost indexeru kontroluje kolekci chyb \_, aby bylo možné zjistit, zda obsahuje klíč, který odpovídá názvu vlastnosti předané indexeru. Není-li k této vlastnosti přidružena žádná chyba ověřování, je vrácen prázdný řetězec.

Nemusíte upravovat domovský kontroler tak, aby bylo možné použít upravenou třídu filmu. Stránka zobrazená na obrázku 3 ukazuje, co se stane, když pro pole názvu nebo formuláře režiséra není zadána žádná hodnota.

[Automatické vytváření metod akcí ![](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)

**Obrázek 03**: formulář s chybějícími hodnotami ([kliknutím zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))

Všimněte si, že hodnota DateReleased je automaticky ověřena. Vzhledem k tomu, že vlastnost DateReleased nepřijímá hodnoty NULL, vygeneruje DefaultModelBinder chybu ověřování pro tuto vlastnost automaticky, pokud nemá hodnotu. Pokud chcete změnit chybovou zprávu pro vlastnost DateReleased, musíte vytvořit vlastní pořadač modelů.

## <a name="summary"></a>Souhrn

V tomto kurzu jste zjistili, jak používat rozhraní IDataErrorInfo k vytváření chybových zpráv ověřování. Nejprve jsme vytvořili částečnou třídu filmu, která rozšiřuje funkčnost třídy částečného filmu vygenerované Entity Framework. Dále jsme přidali logiku ověřování pro částečné metody třídy film OnTitleChanging () a OnDirectorChanging (). Nakonec jsme implementovali rozhraní IDataErrorInfo, aby se tyto ověřovací zprávy daly vystavit do architektury ASP.NET MVC.

> [!div class="step-by-step"]
> [Předchozí](performing-simple-validation-cs.md)
> [Další](validating-with-a-service-layer-cs.md)

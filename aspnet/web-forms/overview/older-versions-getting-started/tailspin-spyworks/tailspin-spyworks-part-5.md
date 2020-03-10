---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 'Část 5: obchodní logika | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 5 přidává některé obchodní logiky.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630303"
---
# <a name="part-5-business-logic"></a>5\. část: Obchodní logika

[Jana Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET. Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.
> 
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 5 přidává některé obchodní logiky.

## <a id="_Toc260221671"></a>Přidání některé obchodní logiky

Chceme, aby naše možnosti nákupu byly dostupné vždycky, když někdo navštíví náš web. Návštěvníci budou moci procházet a přidávat položky do nákupního košíku i v případě, že nejsou registrováni nebo přihlášeni. Až budou připravené k registraci, budou mít možnost ověřit a pokud ještě nejsou členy, budou moci vytvořit účet.

To znamená, že bude nutné implementovat logiku pro převod nákupního košíku z anonymního na stav "registrovaný uživatel".

Pojďme vytvořit adresář s názvem "Classes", potom klikněte pravým tlačítkem myši na složku a vytvořte nový soubor "Class" s názvem MyShoppingCart.cs

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

Jak už jsme uvedli, rozšíříme třídu, která implementuje stránku MyShoppingCart. aspx, a my to provedeme pomocí. ČISTOU výkonnou konstrukci "částečné třídy".

Vygenerované volání pro náš soubor MyShoppingCart.aspx.cf vypadá takto.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

Všimněte si použití klíčového slova Partial.

Soubor třídy, který jsme právě vygenerovali, vypadá takto.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

Naše implementace sloučíme přidáním klíčového slova Partial do tohoto souboru.

Náš nový soubor třídy teď vypadá takto.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

První metoda, kterou přidáme do naší třídy, je metoda AddItem. Toto je metoda, která bude nakonec volána, když uživatel klikne na odkazy přidat do kresby na stránce seznam produktů a podrobnosti o produktu.

V horní části stránky přidejte následující příkazy using.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

A přidejte tuto metodu do třídy MyShoppingCart.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

Používáme LINQ to Entities k zobrazení, zda je položka na košíku již. Pokud ano, aktualizujeme množství objednávky položky, jinak vytvoříme novou položku pro vybranou položku.

Aby bylo možné zavolat tuto metodu, implementujeme stránku AddToCart. aspx, která nejenom třídí tuto metodu, ale po přidání této položky se pak zobrazí aktuální nákupy a = košík.

V Průzkumníku řešení klikněte pravým tlačítkem myši na název řešení a přidejte a přidejte novou stránku s názvem AddToCart. aspx, jak jsme to udělali dříve.

I když jsme tuto stránku mohli použít k zobrazení dočasných výsledků, jako jsou problémy s nízkými zásobami atd. v naší implementaci se stránka ve skutečnosti nevykresluje, ale místo toho se zavolá do logiky Add a Redirect.

K tomuto účelu přidáme následující kód do události\_načíst stránku.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

Všimněte si, že produkt načítáme k přidání do nákupního košíku z parametru QueryString a voláním metody AddItem naší třídy.

Za předpokladu, že se nevyskytnou žádné chyby, řízení se předává na stránku SHoppingCart. aspx, kterou budeme plně implementovat. Pokud by měla být chyba, vyvolali výjimku.

V současné době jsme ještě neimplementovali globální obslužnou rutinu chyb, takže by tato výjimka nebyla ošetřená naší aplikací, ale tuto chvíli nasadíme.

Všimněte si také použití příkazu Debug. selžou () (k dispozici prostřednictvím `using System.Diagnostics;)`

Je aplikace spuštěna v ladicím programu, tato metoda zobrazí podrobný dialog s informacemi o stavu aplikace spolu s chybovou zprávou, kterou zadáte.

Při spuštění v produkčním prostředí se příkaz Debug. selžou () ignoruje.

Všimněte si, že kód nad voláním metody v názvech tříd nákupního košíku "GetShoppingCartId".

Přidejte kód pro implementaci metody následujícím způsobem.

Všimněte si, že jsme také přidali tlačítka aktualizace a rezervace a popisek, kde můžeme zobrazit kartu "celkem".

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

Nyní můžeme přidat položky do nákupního košíku, ale neimplementovali jsme logiku pro zobrazení košíku po přidání produktu.

Proto na stránce MyShoppingCart. aspx přidáte ovládací prvek EntityDataSource a ovládací prvek GridVire následujícím způsobem.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

Zavolejte formulář v návrháři, abyste mohli dvakrát kliknout na tlačítko Aktualizovat košík a generovat obslužnou rutinu události Click, která je zadána v deklaraci v označení.

Podrobnosti budeme implementovat později, ale to nám umožní sestavit a spustit naši aplikaci bez chyb.

Když aplikaci spustíte a přidáte ji do nákupního košíku, zobrazí se tato položka.

![](tailspin-spyworks-part-5/_static/image2.jpg)

Všimněte si, že jsme se odchýlit od výchozího zobrazení mřížky implementací tří vlastních sloupců.

První je editovatelné pole "vázané" množství:

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

Další je "počítaný" sloupec, který zobrazuje celkovou položku řádku (náklady za položku, kolikrát se množství má seřadit):

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

Nakonec máme vlastní sloupec, který obsahuje ovládací prvek CheckBox, který bude uživatel používat k označení toho, že by měla být položka z nákupního grafu odebrána.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

Jak vidíte, řádek celková objednávka je prázdný, takže přidáváme logiku pro výpočet celkového počtu objednávek.

Nejdříve implementujeme metodu gettotal pro naši třídu MyShoppingCart.

Do souboru MyShoppingCart.cs přidejte následující kód.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

Potom na stránce\_načíst obslužnou rutinu události můžeme zavolat naši metodu gettotal. SOUČASNĚ přidáme test, abyste zjistili, jestli je nákupní košík prázdný, a pokud je zobrazený, upravte zobrazení podle potřeby.

Když se teď nákupní košík vyprázdní, získáme toto:

![](tailspin-spyworks-part-5/_static/image4.jpg)

A pokud ne, uvidíme celkový počet.

![](tailspin-spyworks-part-5/_static/image5.jpg)

Tato stránka ale ještě není dokončená.

K přepočítání nákupního košíku budeme potřebovat další logiku odebráním položek označených k odebrání a určením nových hodnot množství, které mohl uživatel v mřížce změnit.

Umožňuje přidat metodu "RemoveItem" do naší třídy nákupního košíku v MyShoppingCart.cs pro zpracování případu, když uživatel označí položku k odebrání.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

Nyní můžeme pracovat jako způsob, jak zpracovat situaci, když uživatel jednoduše změní kvalitu, která má být seřazena v prvku GridView.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

Se základními funkcemi odebrání a aktualizace můžeme implementovat logiku, která ve skutečnosti aktualizuje nákupní košík v databázi. (V MyShoppingCart.cs)

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

Všimněte si, že tato metoda očekává dva parametry. Jednou z nich je ID nákupního košíku a druhý je pole objektů uživatelsky definovaného typu.

Proto pro minimalizaci závislostí naší logiky o specifických uživatelských rozhraních jsme definovali datovou strukturu, kterou můžeme použít k předání položek nákupního košíku do našeho kódu bez toho, aby byla metoda, která potřebuje přímý přístup k ovládacímu prvku GridView.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

V našem souboru MyShoppingCart.aspx.cs můžeme použít tuto strukturu v našem tlačítku aktualizace klikněte níže na obslužnou rutinu události. Všimněte si, že kromě aktualizace košíku aktualizujeme také celkové množství košíku.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

Všimněte si, že konkrétního zájmu tohoto řádku kódu:

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

GetValues () je speciální pomocná funkce, která bude implementována v MyShoppingCart.aspx.cs následujícím způsobem.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

To poskytuje čistě způsob, jak získat přístup k hodnotám vázaných prvků v našem ovládacím prvku GridView. Vzhledem k tomu, že je ovládací prvek CheckBox odebrat položku nevázaný, k němu přistupujeme prostřednictvím metody FindControl ().

V této fázi vývoje projektu se připravujeme k implementaci procesu registrace.

Než to uděláte, využijte Visual Studio k vygenerování databáze členství a přidání uživatele do úložiště členství.

> [!div class="step-by-step"]
> [Předchozí](tailspin-spyworks-part-4.md)
> [Další](tailspin-spyworks-part-6.md)

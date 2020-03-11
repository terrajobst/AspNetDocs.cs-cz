---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
title: Vytvoření vlastního zařízení Extended ovládacího prvku AJAX Control Toolkit (VB) | Microsoft Docs
author: microsoft
description: Vlastní rozšířené ovládací prvky umožňují přizpůsobit a roztáhnout možnosti ovládacích prvků ASP.NET bez nutnosti vytvářet nové třídy.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 18b29834-c991-4e0c-b533-44d358fbfc9c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 0849fa6c13679e0cd01bb20a4067a097acbce298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578160"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-vb"></a>Vytvoření vlastního rozšiřujícího ovládacího prvku AJAX Control Toolkit (VB)

od [Microsoftu](https://github.com/microsoft)

> Vlastní rozšířené ovládací prvky umožňují přizpůsobit a roztáhnout možnosti ovládacích prvků ASP.NET bez nutnosti vytvářet nové třídy.

V tomto kurzu se naučíte, jak vytvořit vlastní zařízení pro ovládání ovládacího prvku AJAX Control Toolkit. Vytvoříme jednoduché, ale užitečné nové zařízení, které změní stav tlačítka z zakázáno na povoleno, když zadáte text do textového pole. Po přečtení tohoto kurzu budete moct ASP.NET sadu nástrojů AJAX rozšiřuje o své vlastní ovládací prvky.

Pomocí sady Visual Studio nebo aplikace Visual Web Developer můžete vytvořit vlastní ovládací prvky ovládacího prvku a (Ujistěte se, že máte nejnovější verzi aplikace Visual Web Developer).

## <a name="overview-of-the-disabledbutton-extender"></a>Přehled zařízení DisabledButton

Náš nový rozšířený ovládací prvek se jmenuje jako DisabledButton. Tento ovládací prvek bude mít tři vlastnosti:

- Vlastnost TargetControlID prvku – textové pole, které ovládací prvek rozšiřuje.
- TargetButtonIID – zakázané nebo povolené tlačítko.
- DisabledText – text, který je původně zobrazený na tlačítku. Když začnete psát, tlačítko zobrazí hodnotu vlastnosti text tlačítka.

Připojíte zařízení DisabledButton k ovládacímu prvku TextBox a tlačítko. Před zadáním libovolného textu je tlačítko zakázané a textové pole a tlačítko vypadá takto:

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image1.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image3.png))

Po zahájení psaní textu je tlačítko povolené a textové pole a tlačítko vypadá takto:

[![](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image4.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image6.png))

Abychom mohli vytvořit náš ovládací prvek pro rozšiřování ovládacího prvku, musíme vytvořit následující tři soubory:

- DisabledButtonExtender. vb – tento soubor je třída ovládacího prvku na straně serveru, která bude spravovat vytváření zařízení a umožňuje vám nastavit vlastnosti v době návrhu. Definuje také vlastnosti, které lze nastavit v zařízení. Tyto vlastnosti jsou přístupné prostřednictvím kódu a v době návrhu a odpovídají vlastnostem definovaným v souboru DisableButtonBehavior. js.
- DisabledButtonBehavior. js – tento soubor vám umožní přidat veškerou logiku klientského skriptu.
- DisabledButtonDesigner. vb – Tato třída umožňuje funkce v době návrhu. Tuto třídu budete potřebovat, pokud chcete, aby měl ovládací prvek zařízení správně fungovat s návrhářem sady Visual Studio/Visual Web Developer.

Proto se rozšiřuje ovládací prvek ovládacího prvku na straně serveru, chování na straně klienta a Třída návrháře na straně serveru. Naučíte se, jak vytvořit všechny tři tyto soubory v následujících oddílech.

## <a name="creating-the-custom-extender-website-and-project"></a>Vytvoření vlastního webu a projektu rozšířené aplikace

Prvním krokem je vytvoření projektu knihovny tříd a webu v aplikaci Visual Studio nebo Visual Web Developer. Vytvoříme vlastní zařízení pro rozšiřování v projektu knihovny tříd a otestuji vlastní zařízení na webu.

Pojďme s webem začít. K vytvoření webu použijte následující postup:

1. Vyberte soubor možnosti nabídky **, nový web**.
2. Vyberte šablonu webu **ASP.NET** .
3. Pojmenujte nový web *WEB1*.
4. Klikněte na tlačítko **OK**.

Dále je potřeba vytvořit projekt knihovny tříd, který bude obsahovat kód pro ovládací prvek Extender ovládacího prvku:

1. Vyberte položku nabídky **soubor, přidat, nový projekt**.
2. Vyberte šablonu **knihovny tříd** .
3. Pojmenujte novou knihovnu tříd s názvem **CustomExtenders**.
4. Klikněte na tlačítko **OK**.

Po dokončení tohoto postupu by okno Průzkumník řešení mělo vypadat jako obrázek 1.

[![řešení s projektem webu a knihovny tříd](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image7.png)

**Obrázek 01**: řešení s projektem webu a knihovny tříd ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image9.png))

Dále je nutné přidat všechny nezbytné odkazy na sestavení do projektu knihovny tříd:

1. Klikněte pravým tlačítkem na projekt CustomExtenders a vyberte možnost nabídky **Přidat odkaz**.
2. Vyberte kartu .NET.
3. Přidejte odkazy na následující sestavení:

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. Vyberte kartu Procházet.
5. Přidejte odkaz na sestavení AjaxControlToolkit. dll. Toto sestavení je umístěno ve složce, do které jste stáhli sadu nástrojů AJAX Control Toolkit.

Můžete ověřit, že jste přidali všechny správné odkazy kliknutím pravým tlačítkem myši na projekt, výběrem vlastností a kliknutím na kartu odkazy (viz obrázek 2).

[![odkazuje na složku s požadovanými odkazy](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image10.png)

**Obrázek 02**: odkazy na složku s požadovanými odkazy ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image12.png))

## <a name="creating-the-custom-control-extender"></a>Vytvoření zařízení pro ovládání vlastního ovládacího prvku

Teď, když máme naši knihovnu tříd, můžeme začít sestavovat ovládací prvek pro rozšiřování. Pojďme začít s holémi kostimi vlastní třídy ovládacího prvku pro rozšířené ovládací prvky (viz výpis 1).

**Výpis 1 – MyCustomExtender. vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample1.vb)]

Existuje několik věcí, které se týkají třídy Extender ovládacího prvku v seznamu 1. Nejprve si všimněte, že třída dědí ze základní třídy ExtenderControlBase. Z této základní třídy jsou odvozeny všechny ovládací prvky pro rozšířené ovládací prvky AJAX Control Toolkit. Například základní třída zahrnuje vlastnost TargetID, která je povinnou vlastností každého zařízení v rozšířeném ovládacím prvku.

Dále si všimněte, že třída obsahuje následující dva atributy, které se vztahují ke skriptu klienta:

- WebResource – způsobí, že se soubor zahrne do sestavení jako vložený prostředek.
- ClientScriptResource – způsobí, že se prostředek skriptu načte ze sestavení.

Atribut WebResource se používá k vložení souboru JavaScriptu MyControlBehavior. js do sestavení při kompilaci vlastního zařízení. Atribut ClientScriptResource se používá k načtení skriptu MyControlBehavior. js ze sestavení při použití vlastního zařízení na webové stránce.

Aby atributy WebResource a ClientScriptResource fungovaly, je nutné zkompilovat soubor JavaScriptu jako vložený prostředek. V okně Průzkumník řešení vyberte soubor, otevřete seznam vlastností a přiřaďte hodnotu *vloženého prostředku* k vlastnosti **Akce sestavení** .

Všimněte si, že ovládací prvek Extender obsahuje také Atribut TargetControlType. Tento atribut slouží k určení typu ovládacího prvku, který je rozšířen rozšiřujícím ovládacím prvkem. V případě výpisu 1 se k rozšiřování textového pole používá ovládací prvek Extender ovládacího prvku.

Nakonec si všimněte, že vlastní ovládací prvek obsahuje vlastnost s názvem MyProperty. Vlastnost je označena atributem ExtenderControlProperty. Metody GetPropertyValue () a SetPropertyValue () slouží k předání hodnoty vlastnosti ze serveru rozšířených ovládacím prvkem do chování na straně klienta.

Nechte si pokračovat a implementujte kód pro náš DisabledButton. Kód pro tohoto zařízení Extender najdete v seznamu 2.

**Výpis 2-DisabledButtonExtender. vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample2.vb)]

DisabledButton rozšířil v seznamu 2 má dvě vlastnosti s názvem TargetButtonID a DisabledText. IDReferenceProperty, který se použije na vlastnost TargetButtonID, vám zabrání v přiřazení jakékoli jiné než ID ovládacího prvku tlačítko k této vlastnosti.

Atributy WebResource a ClientScriptResource přidružuje chování na straně klienta umístěné v souboru s názvem DisabledButtonBehavior. js pomocí tohoto zařízení. Tento soubor JavaScriptu probereme v další části.

## <a name="creating-the-custom-extender-behavior"></a>Vytváření vlastního zařízení s rozšířeným chováním

Komponenta na straně klienta ovládacího prvku pro rozšiřování se nazývá chování. Skutečná logika pro zakázání a povolení tlačítka je obsažena v chování DisabledButton. Kód JavaScriptu pro chování je zahrnutý v seznamu 3.

**Výpis 3-DisabledButton. js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample3.js)]

Soubor JavaScriptu v seznamu 3 obsahuje třídu na straně klienta s názvem DisabledButtonBehavior. Tato třída, jako je například její vlákna na straně serveru, zahrnuje dvě vlastnosti s názvem TargetButtonID a DisabledText, ke kterým můžete přistupovat pomocí Get\_TargetButtonID/set\_TargetButtonID a získat\_DisabledText/set\_DisabledText.

Metoda Initialize () přidruží obslužnou rutinu události KeyUp k cílovému elementu pro chování. Pokaždé, když zadáte písmeno do textového pole přidruženého k tomuto chování, spustí se obslužná rutina KeyUp. Obslužná rutina KeyUp buď povolí nebo zakáže tlačítko v závislosti na tom, zda textové pole přidružené k chování obsahuje libovolný text.

Nezapomeňte, že soubor JavaScriptu musíte zkompilovat v seznamu 3 jako vložený prostředek. V okně Průzkumník řešení vyberte soubor, otevřete seznam vlastností a přiřaďte hodnotu *vložený prostředek* k vlastnosti **Akce sestavení** (viz obrázek 3). Tato možnost je k dispozici v aplikaci Visual Studio i v aplikaci Visual Web Developer.

[![přidání souboru JavaScriptu jako vloženého prostředku](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image13.png)

**Obrázek 03**: Přidání souboru JavaScriptu jako vloženého prostředku ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image15.png))

## <a name="creating-the-custom-extender-designer"></a>Vytvoření vlastního návrháře rozšířeného objektu

Existuje jedna poslední třída, kterou musíme vytvořit k dokončení našeho zařízení. Musíme vytvořit třídu návrháře v seznamu 4. Tato třída je nutná k tomu, aby se zařízení správně chovalo s návrhářem sady Visual Studio nebo Visual Web Developer.

**Výpis 4 – DisabledButtonDesigner. vb**

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample4.vb)]

Přiřadíte návrháře v seznamu 4 s nástrojem DisabledButton Extender s atributem Designer. Je nutné použít atribut návrháře pro třídu DisabledButtonExtender, například:

[!code-vb[Main](creating-a-custom-ajax-control-toolkit-control-extender-vb/samples/sample5.vb)]

## <a name="using-the-custom-extender"></a>Používání vlastního zařízení pro rozšiřování

Teď, když jsme dokončili vytváření zařízení DisabledButton Control, je čas ho použít na našem webu ASP.NET. Nejdřív je potřeba přidat do sady nástrojů vlastní ovládací prvek. Postupujte následovně:

1. Otevřete stránku ASP.NET dvojitým kliknutím na stránku v okně Průzkumník řešení.
2. Klikněte pravým tlačítkem myši na panel nástrojů a vyberte možnost nabídky vybrat **položky**.
3. V dialogovém okně zvolit položky sady nástrojů přejděte do sestavení CustomExtenders. dll.
4. Kliknutím na tlačítko **OK** zavřete dialogové okno.

Po dokončení tohoto postupu by se měl ovládací prvek DisabledButton ovládacího prvku v sadě nástrojů Zobrazit (viz obrázek 4).

[![DisabledButton v sadě nástrojů](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image16.png)

**Obrázek 04**: DisabledButton v sadě nástrojů ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image18.png))

Dál je potřeba vytvořit novou stránku ASP.NET. Postupujte následovně:

1. Vytvořte novou stránku ASP.NET s názvem ShowDisabledButton. aspx.
2. Přetáhněte ScriptManager na stránku.
3. Přetáhněte na stránku ovládací prvek TextBox.
4. Přetáhněte na stránku ovládací prvek tlačítko.
5. V okno Vlastnosti změňte vlastnost ID tlačítka na hodnotu <em>btnSave</em> a vlastnost text na hodnotu *Uložit\** .

Vytvořili jsme stránku se standardním textovým polem a ovládacím prvkem tlačítko ASP.NET.

Dál je potřeba, abyste ovládací prvek TextBox rozšířili pomocí nástroje DisabledButton Extender:

1. Kliknutím na možnost **přidat rozšířenou** úlohu otevřete dialogové okno Průvodce rozšířeným nastavením (viz obrázek 5). Všimněte si, že dialog obsahuje naše vlastní zařízení DisabledButton.
2. Vyberte zařízení DisabledButton a klikněte na tlačítko **OK** .

[![dialogovém okně Průvodce roztažením](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image19.png)

**Obrázek 05**: dialogové okno Průvodce roztažením ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image21.png))

Nakonec můžeme nastavit vlastnosti zařízení DisabledButton. Vlastnosti zařízení DisabledButton můžete upravit úpravou vlastností ovládacího prvku TextBox:

1. Vyberte textové pole v návrháři.
2. V okno Vlastnosti rozbalte uzel rozšiřující objekty (viz obrázek 6).
3. Přiřaďte hodnotu *Uložit* do vlastnosti DisabledText a hodnotu *BtnSave* na vlastnost TargetButtonID.

[![nastavení vlastností zařízení](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image22.png)

**Obrázek 6**: nastavení vlastností rozšířeného objektu ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image24.png))

Po spuštění stránky (po stisknutí klávesy F5) je ovládací prvek tlačítko zpočátku zakázán. Jakmile začnete zadávat text do textového pole, je ovládací prvek tlačítko povolen (viz obrázek 7).

[![zařízení DisabledButton v akci](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image25.png)

**Obrázek 07**: DisabledButton, který se nachází v akci ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-custom-ajax-control-toolkit-control-extender-vb/_static/image27.png))

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu bylo vysvětlit, jak můžete sadu nástrojů AJAX Control Toolkit pomocí vlastních ovládacích prvků rozšířené ovládací prvky roztáhnout. V tomto kurzu jsme vytvořili jednoduchý DisabledButton ovládacího prvku pro rozšiřování. Toto zařízení jsme implementovali vytvořením třídy DisabledButtonExtender, chováním JavaScriptu DisabledButtonBehavior a třídy DisabledButtonDesigner. Podobnou sadu kroků vydržíte vždy, když vytvoříte zařízení pro vlastní ovládací prvek.

> [!div class="step-by-step"]
> [Předchozí](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)

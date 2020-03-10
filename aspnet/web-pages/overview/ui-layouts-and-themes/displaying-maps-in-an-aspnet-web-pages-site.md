---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: Zobrazení map na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek vysvětluje, jak zobrazit interaktivní mapy na stránkách na webu ASP.NET Web Pages (Razor) na základě mapování služeb poskytovaných bingem, Google, MA...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638675"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a>Zobrazení map na webu ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak zobrazit interaktivní mapy na stránkách na webu ASP.NET Web Pages (Razor) na základě mapování služeb poskytovaných bingem, Google, MapQuest a Yahoo.
> 
> Naučíte se:
> 
> - Generování mapy založené na adrese.
> - Jak vygenerovat mapu na základě souřadnic zeměpisné šířky a délky.
> - Jak zaregistrovat vývojářský účet mapy Bing a získat klíč pro použití se službou mapy Bing.
> 
> Toto je funkce ASP.NET představená v článku:
> 
> - Pomocná rutina `Maps`
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - WebMatrix 2
>   
> 
> V tomto kurzu se používá také WebMatrix 3.

Na webových stránkách můžete zobrazit mapy na stránce pomocí pomocné rutiny `Maps`. Můžete vygenerovat mapy založené na adrese nebo v sadě souřadnic Zeměpisná délka a zeměpisná šířka. Třída `Maps` umožňuje volat oblíbené mapové moduly, včetně Bingu, Google, MapQuest a Yahoo.

Postup pro přidání mapování na stránku je stejný bez ohledu na to, které mapové moduly voláte. Stačí přidat odkaz na soubor JavaScriptu, který zpřístupňuje dostupné metody pro zobrazení mapy, a potom zavoláte metody pomocné rutiny `Maps`.

Můžete zvolit službu mapování na základě toho, kterou `Maps` pomocnou metodu použijete. Můžete použít některý z těchto kroků:

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a>Instalace potřebných částí

K zobrazení map budete potřebovat tyto části:

- Pomocná rutina `Maps` Tato pomoc je ve verzi 2 knihovny webových pomoců ASP.NET. Pokud jste ještě knihovnu nepřidali, můžete ji nainstalovat na svůj web jako balíček NuGet. Podrobnosti najdete v tématu [instalace pomocníků na webu webové stránky ASP.NET](https://go.microsoft.com/fwlink/?LinkId=252372). (V galerii vyhledejte balíček `microsoft-web-helpers`.)
- Knihovna jQuery. Několik šablon webu WebMatrix již obsahuje knihovny jQuery ve složkách *skriptu* . Pokud tyto knihovny nemáte, můžete si stáhnout nejnovější knihovnu jQuery přímo z webu [jQuery.org](http://jQuery.org) . Můžete také vytvořit novou lokalitu pomocí šablony (například šablony **webu Starter** ) a potom zkopírovat soubory jQuery z dané lokality do aktuální lokality.

Nakonec, pokud chcete používat mapy Bing, musíte nejdřív vytvořit (bezplatný) účet a získat klíč. Klíč získáte pomocí následujících kroků:

1. Vytvořte účet na [účtu vývojáře pro mapy Bing](https://www.microsoft.com/maps/developers/web.aspx). Musíte mít také účet Microsoft (Windows Live ID).

    Můžete určit, že chcete použít klíč pro **vyhodnocení a testování**. Pokud testujete funkci mapování na vlastním počítači pomocí WebMatrixu a IIS Express, Projděte si pracovní prostor **webu** a poznamenejte si adresu URL vašeho webu (například `http://localhost:50408`, i když se vaše číslo portu bude pravděpodobně lišit). Tuto adresu *localhost* můžete použít jako web při registraci.
2. Po registraci účtu přejděte do centra účtů mapy Bing a klikněte na tlačítko **vytvořit nebo zobrazit klíče**:

    ![mapování – 2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. Poznamenejte si klíč, který Bing vytvoří.

## <a name="creating-a-map-based-on-an-address-using-google"></a>Vytvoření mapy na základě adresy (pomocí Google)

Následující příklad ukazuje, jak vytvořit stránku, která vykresluje mapu na základě adresy. Tento příklad ukazuje, jak používat Google Maps.

1. V kořenovém adresáři webu vytvořte soubor s názvem *MapAddress. cshtml* . Tato stránka vygeneruje mapu založenou na adrese, kterou jí předáte.
2. Zkopírujte do souboru následující kód, který přepíše existující obsah.

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    Všimněte si následujících funkcí stránky:

    - Prvek `<script>` v elementu `<head>`. V příkladu element `<script>` odkazuje na soubor *jQuery 1.6.4. min. js* , což je minifikovaného (komprimovaná) verze knihovny jQuery, verze 1.6.4. Všimněte si, že odkaz předpokládá, že soubor *. js* je ve složce *Scripts* vaší lokality. 

        > [!NOTE]
        > Pokud používáte jinou verzi knihovny jQuery, stačí, abyste se ujistili, že budete správně ukazovat na správnou verzi.
    - Volání `@Maps.GetGoogleHtml` v těle stránky. Chcete-li namapovat adresu, je nutné předat řetězec adresy. Metody pro ostatní mapové stroje fungují podobným způsobem (`@Maps.GetYahooHtml``@Maps.GetMapQuestHtml`).
3. Spusťte stránku a zadejte adresu. Stránka zobrazuje mapu založenou na Google Maps, která zobrazuje umístění, které jste zadali.

     ![mapování – 1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a>Vytvoření mapy na základě souřadnic zeměpisné šířky a délky (pomocí Bingu)

Tento příklad ukazuje, jak vytvořit mapu založenou na souřadnicích. Tento příklad ukazuje, jak používat mapy Bing a jak klíč Bingu zahrnout. (Můžete také vytvořit mapu založenou na souřadnicích pomocí jiných mapových modulů, a to bez použití klíče Bingu.)

1. V kořenovém adresáři lokality vytvořte soubor s názvem *MapCoordinates. cshtml* a nahraďte stávající obsah následujícím kódem a označením:

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. Nahraďte `your-key-here` klíčem mapy Bing, který jste předtím vygenerovali.
3. Spusťte stránku *MapCoordinates. cshtml* , zadejte souřadnice zeměpisné šířky a délky a potom klikněte na **mapu IT!** . . (Pokud neznáte žádné souřadnice, zkuste následující. Toto je umístění v areálu Microsoft Redmond.)

   - Zeměpisná šířka: 47.6781005859375
   - Zeměpisná délka: – 122.158317565918

     Stránka se zobrazí pomocí souřadnic, které jste zadali.

     ![mapování – 3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

[Reference k rozhraní API Microsoft. Maps](https://msdn.microsoft.com/library/gg427611.aspx)

---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: Vytváření rozložení stránek pomocí stránek předlohy pro zobrazení (VB) | Microsoft Docs
author: microsoft
description: V tomto kurzu se naučíte, jak vytvořit společné rozložení stránky pro více stránek ve vaší aplikaci tím, že využijete možnosti Zobrazit stránky předlohy. Můžete použít...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 97c0ecf1953cc54030656dd710a5150243877110
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541221"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a>Vytvoření rozložení stránek pomocí stránek předlohy pro zobrazení (VB)

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> V tomto kurzu se naučíte, jak vytvořit společné rozložení stránky pro více stránek ve vaší aplikaci tím, že využijete možnosti Zobrazit stránky předlohy. Můžete použít stránku zobrazení předlohy, například k definování rozložení stránky se dvěma sloupci a použít rozložení dvou sloupců pro všechny stránky ve vaší webové aplikaci.

## <a name="creating-page-layouts-with-view-master-pages"></a>Vytváření rozložení stránek pomocí stránek předlohy pro zobrazení

V tomto kurzu se naučíte, jak vytvořit společné rozložení stránky pro více stránek ve vaší aplikaci tím, že využijete možnosti Zobrazit stránky předlohy. Můžete použít stránku zobrazení předlohy, například k definování rozložení stránky se dvěma sloupci a použít rozložení dvou sloupců pro všechny stránky ve vaší webové aplikaci.

Můžete také využít výhod zobrazení stránky předloh pro sdílení společného obsahu napříč několika stránkami v aplikaci. Můžete například umístit logo webu, navigační odkazy a reklamy banneru na stránku zobrazení předlohy. Díky tomu budou mít všechny stránky v aplikaci automaticky tento obsah zobrazovat.

V tomto kurzu se dozvíte, jak vytvořit novou stránku předlohy zobrazení a vytvořit novou stránku zobrazení obsahu založenou na stránce předlohy.

### <a name="creating-a-view-master-page"></a>Vytvoření hlavní stránky zobrazení

Pojďme začít vytvořením hlavní stránky zobrazení, která definuje rozložení se dvěma sloupci. Novou stránku zobrazení předlohy přidáte do projektu MVC kliknutím pravým tlačítkem myši na složku Views\Shared, vybráním možnosti nabídky **Přidat, nová položka**a výběrem šablony stránky předlohy zobrazení MVC (viz obrázek 1).

[![přidávání řídicí stránky zobrazení](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**Obrázek 01**: Přidání stránky předlohy zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))

V aplikaci můžete vytvořit více než jednu vzorovou stránku zobrazení. Každé zobrazení stránky předlohy může definovat jiné rozložení stránky. Například může být vhodné, aby některé stránky měly rozložení se dvěma sloupci a další stránky, které mají rozložení se třemi sloupci.

Stránka zobrazení předlohy vypadá velmi podobně jako standardní zobrazení ASP.NET MVC. Na rozdíl od normálního zobrazení však stránka zobrazení předlohy obsahuje jednu nebo více značek `<asp:ContentPlaceHolder>`. Značky `<contentplaceholder>` slouží k označení oblastí stránky předlohy, které mohou být přepsány na jednotlivých stránkách obsahu.

Například stránka zobrazení předlohy v seznamu 1 definuje rozložení se dvěma sloupci. Obsahuje dvě `<contentplaceholder>` značky. Jeden `<ContentPlaceHolder>` pro každý sloupec.

**Výpis 1 – `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

Tělo stránky předlohy zobrazení v seznamu 1 obsahuje dvě značky `<div>`, které odpovídají dvěma sloupcům. Třída sloupce kaskádová šablona stylů se aplikuje na `<div>` značek. Tato třída je definována v šabloně stylů deklarované v horní části stránky předlohy. Můžete zobrazit náhled, jak se stránka zobrazení předlohy vykreslí přechodem na zobrazení Návrh. Klikněte na kartu Návrh v levém dolním rohu editoru zdrojového kódu (viz obrázek 2).

[![zobrazení náhledu stránky předlohy v Návrháři](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**Obrázek 02**: zobrazení náhledu stránky předlohy v Návrháři ([kliknutím zobrazíte obrázek v plné velikosti](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))

### <a name="creating-a-view-content-page"></a>Vytvoření stránky zobrazení obsahu

Po vytvoření stránky předlohy pro zobrazení můžete vytvořit jednu nebo více stránek obsahu zobrazení na základě stránky zobrazení předlohy. Můžete například vytvořit stránku obsahu zobrazení indexu pro domovskou kartu tak, že kliknete pravým tlačítkem na složku Views\Home, vyberete **Přidat, nová položka**, vyberete šablonu **stránky obsahu zobrazení MVC** , zadáte název index. aspx a kliknete na tlačítko Přidat (viz obrázek 3).

[![přidávání stránky zobrazení obsahu](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**Obrázek 03**: Přidání stránky zobrazení obsahu ([kliknutím zobrazíte obrázek v plné velikosti](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))

Po kliknutí na tlačítko Přidat se zobrazí nové dialogové okno, ve kterém můžete vybrat stránku předlohy pro zobrazení, kterou chcete přidružit k stránce zobrazení obsahu (viz obrázek 4). Můžete přejít na stránku předlohy zobrazení Web. Master, kterou jsme vytvořili v předchozí části.

[![výběru stránky předlohy](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**Obrázek 04**: Výběr stránky předlohy ([kliknutím zobrazíte obrázek v plné velikosti](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))

Po vytvoření nové stránky pro zobrazení obsahu na základě hlavní stránky site. Master získáte soubor v seznamu 2.

**Výpis 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

Všimněte si, že toto zobrazení obsahuje značku `<asp:Content>`, která odpovídá každé z značek `<asp:ContentPlaceHolder>` na stránce zobrazení předlohy. Každá značka `<asp:Content>` obsahuje atribut ContentPlaceHolderID, který odkazuje na konkrétní `<asp:ContentPlaceHolder>`, který Přepisuje.

Všimněte si, že stránka zobrazení obsahu v seznamu 2 neobsahuje normální otevírání a zavírání značek HTML. Například neobsahuje úvodní a uzavírací `<html>` ani značky `<head>`. Všechny normální značky otevírání a zavírání jsou obsaženy na stránce zobrazení předlohy.

Veškerý obsah, který chcete zobrazit na stránce zobrazení obsahu, musí být umístěn v rámci značky `<asp:Content>`. Pokud umístíte libovolný HTML nebo jiný obsah mimo tyto značky, zobrazí se při pokusu o zobrazení stránky chyba.

Nemusíte potlačit každou `<asp:ContentPlaceHolder>`ovou značku ze stránky předlohy na stránce zobrazení obsahu. Pokud chcete značku nahradit určitým obsahem, stačí přepsat značku `<asp:ContentPlaceHolder>`.

Například změněné zobrazení indexu v seznamu 3 obsahuje pouze dvě značky `<asp:Content>`. Každá z `<asp:Content>` značek obsahuje nějaký text.

**Výpis 3 – `Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

Po vyžádání zobrazení v seznamu 3 se stránka vykreslí na obrázku 5. Všimněte si, že zobrazení vykresluje stránku se dvěma sloupci. Všimněte si, že obsah ze stránky zobrazení obsahu se sloučí s obsahem ze stránky zobrazení předlohy.

[![stránku obsahu zobrazení indexu](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**Obrázek 05**: stránka zobrazení indexu obsahu ([kliknutím zobrazíte obrázek v plné velikosti](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))

### <a name="modifying-view-master-page-content"></a>Změny zobrazení obsahu stránky předlohy

Jedním z problémů, se kterými se setkáte téměř okamžitě při práci se stránkami zobrazení předloh, je problém s úpravou obsahu stránky předlohy zobrazení, když se vyžadují různé stránky obsahu zobrazení. Například chcete, aby každá stránka ve webové aplikaci měla jedinečný název. Název je však deklarován na stránce zobrazení předlohy a nikoli na stránce zobrazení obsahu. Jak si tedy můžete přizpůsobit nadpis stránky pro jednotlivé stránky obsahu zobrazení?

Existují dva způsoby, jak můžete upravit název zobrazený na stránce zobrazení obsahu. Nejprve můžete přiřadit nadpis stránky k atributu title direktivy `<%@ page %>` deklarované v horní části stránky zobrazení obsahu. Například pokud chcete přiřadit nadpis stránky "Super Skvělé web" do zobrazení indexu, můžete do horní části zobrazení indexu zahrnout následující direktivu:

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

Když se v prohlížeči vykreslí zobrazení indexu, zobrazí se požadovaný nadpis v záhlaví prohlížeče:

[![záhlaví prohlížeče](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)

Je nutné, aby stránka zobrazení předlohy splňovala podmínky, aby atribut title fungoval. Stránka Zobrazit předloha musí obsahovat značku `<head runat="server">` namísto normální `<head>` značky pro její hlavičku. Pokud značka `<head>` nezahrnuje atribut runat = "Server", nadpis se nezobrazí. Výchozí stránka zobrazit předlohu obsahuje požadovanou značku `<head runat="server">`.

Alternativním přístupem k úpravě obsahu stránky předlohy ze stránky obsahu jednotlivých zobrazení je zabalení oblasti, kterou chcete upravit, ve značce `<asp:ContentPlaceHolder>`. Představte si například, že chcete změnit nejen nadpis, ale také metaznačky, vykreslené stránkou zobrazení předlohy. Stránka zobrazení předlohy v seznamu 4 obsahuje značku `<asp:ContentPlaceHolder>` v rámci své `<head>` značky.

**Výpis 4 – `Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

Všimněte si, že značka `<asp:ContentPlaceHolder>` v seznamu 4 obsahuje výchozí obsah: výchozí název a výchozí meta značky. Pokud tuto značku `<asp:ContentPlaceHolder>` nepřepisujete na stránce obsahu individuálního zobrazení, zobrazí se výchozí obsah.

Stránka zobrazení obsahu v seznamu 5 přepíše značku `<asp:ContentPlaceHolder>`, aby zobrazila vlastní název a vlastní metaznačky.

**Výpis 5 – `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>Souhrn

V tomto kurzu jste získali základní informace o zobrazení stránek předlohy a zobrazení stránek obsahu. Zjistili jste, jak vytvořit nové stránky předlohy zobrazení a vytvořit zobrazení stránek obsahu na základě nich. Prozkoumali jsme také, jak můžete upravit obsah stránky předlohy zobrazení z konkrétní stránky obsahu zobrazení.

> [!div class="step-by-step"]
> [Předchozí](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [Další](passing-data-to-view-master-pages-vb.md)

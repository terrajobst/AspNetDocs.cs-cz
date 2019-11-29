---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
title: Použití CascadingDropDown s databází (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v anoth...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 97a3d33c-c856-43f3-8acb-f1ccbc48221a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 4482aa18c4446ec8f5f160c423008398ea2e1d0d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599485"
---
# <a name="using-cascadingdropdown-with-a-database-vb"></a>Použití ovládacího prvku CascadingDropDown s databází (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1VB.pdf)

> Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. Aby to fungovalo, musí být vytvořená speciální webová služba.

## <a name="overview"></a>Přehled

Ovládací prvek CascadingDropDown v sadě nástrojů AJAX Control Toolkit rozšiřuje ovládací prvek DropDownList tak, aby změny v jednom DropDownList načítají přidružené hodnoty v jiné DropDownList. (Například jeden seznam obsahuje seznam stavů USA a další seznam se pak vyplní hlavními městy v tomto stavu.) Aby to fungovalo, musí být vytvořená speciální webová služba.

## <a name="steps"></a>Uvedené

Nejdříve je vyžadován zdroj dat. V této ukázce se používá databáze AdventureWorks a edice Microsoft SQL Server 2005 Express. Databáze je volitelnou součástí instalace sady Visual Studio (včetně Express Edition) a je k dispozici také jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). Databáze AdventureWorks je součástí ukázek SQL Server 2005 a ukázkových databází (Stáhnout v [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit soubor databáze `AdventureWorks.mdf`.

V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení. Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v &lt;`form`elementu &gt;):

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample1.aspx)]

V dalším kroku jsou vyžadovány dva ovládací prvky DropDownList. V této ukázce používáme dodavatele a kontaktní údaje od společnosti AdventureWorks, takže vytvoříme jeden seznam pro dostupné dodavatele a jeden pro dostupné kontakty:

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample2.aspx)]

Pak se na stránku musí přidat dva CascadingDropDowny. Jedna vyplní první seznam (dodavatelé) a druhá vyplní druhý seznam (kontakty). Je nutné nastavit následující atributy:

- `ServicePath`: adresa URL webové služby, která doručuje položky seznamu.
- `ServiceMethod`: Webová metoda doručování položek seznamu
- `TargetControlID`: ID rozevíracího seznamu
- `Category`: informace o kategorii, které se odešlou do webové metody při volání
- `PromptText`: text zobrazený při asynchronním načítání dat seznamu ze serveru
- `ParentControlID`: (nepovinný) nadřazený rozevírací seznam, který aktivuje načítání aktuálního seznamu

V závislosti na použitém programovacím jazyce se změní název příslušné webové služby, ale všechny ostatní hodnoty atributu jsou stejné. Tady je prvek CascadingDropDown pro první rozevírací seznam:

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample3.aspx)]

Rozšířené ovládací prvky pro druhý seznam musí nastavovat atribut `ParentControlID` tak, že výběr položky v seznamu dodavatelů aktivuje načítání přidružených prvků v seznamu kontaktů.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample4.aspx)]

Skutečná práce se pak provede ve webové službě, která je nastavená takto. Všimněte si, že je použit atribut `[ScriptService]`, jinak ASP.NET AJAX nemůže vytvořit proxy JavaScript pro přístup k webovým metodám z kódu skriptu na straně klienta.

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample5.aspx)]

Signatura webových metod, které volá CascadingDropDown, je následující:

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample6.vb)]

Proto návratová hodnota musí být pole typu `CascadingDropDownNameValue`, které je definováno pomocí sady nástrojů Control Toolkit. Metodu `GetVendors()` je poměrně snadno implementovaná: kód se připojuje k databázi AdventureWorks a dotazuje se prvních 25 dodavatelů. První parametr v konstruktoru `CascadingDropDownNameValue` je titulek položky seznamu, druhá jeho hodnota (atribut value v HTML &lt;`option`&gt; element). Zde je kód:

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample7.vb)]

Získání přidružených kontaktů pro dodavatele (název metody: `GetContactsForVendor()`) je trickier bitů. Nejdříve je třeba určit dodavatele, který byl vybrán v prvním rozevíracím seznamu. Sada ovládacích prvků definuje pomocnou metodu pro tuto úlohu: metoda `ParseKnownCategoryValuesString()` vrací `StringDictionary` prvek s daty rozevíracího seznamu:

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample8.vb)]

Z bezpečnostních důvodů musí být tato data nejprve ověřena. Takže pokud existuje položka dodavatele (protože vlastnost `Category` prvního prvku CascadingDropDown je nastavená na `"Vendor"`), může se načíst ID vybraného dodavatele:

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample9.vb)]

Zbývající část metody je poměrně přímá a pak. ID dodavatele se používá jako parametr pro dotaz SQL, který načte všechny přidružené kontakty pro tohoto dodavatele. Znovu metoda vrátí pole typu `CascadingDropDownNameValue`.

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample10.vb)]

Načtěte stránku ASP.NET a po krátké době se seznam dodavatelů vyplní 25 položkami. Vyberte jednu položku a Všimněte si, jak je druhý rozevírací seznam vyplněn daty.

[![se první seznam vyplní automaticky](using-cascadingdropdown-with-a-database-vb/_static/image2.png)](using-cascadingdropdown-with-a-database-vb/_static/image1.png)

První seznam je vyplněn automaticky ([kliknutím zobrazíte obrázek v plné velikosti).](using-cascadingdropdown-with-a-database-vb/_static/image3.png)

[![se druhý seznam vyplní podle výběru v prvním seznamu.](using-cascadingdropdown-with-a-database-vb/_static/image5.png)](using-cascadingdropdown-with-a-database-vb/_static/image4.png)

Druhý seznam je vyplněn podle výběru v prvním seznamu ([kliknutím zobrazíte obrázek v plné velikosti).](using-cascadingdropdown-with-a-database-vb/_static/image6.png)

> [!div class="step-by-step"]
> [Předchozí](filling-a-list-using-cascadingdropdown-vb.md)
> [Další](presetting-list-entries-with-cascadingdropdown-vb.md)

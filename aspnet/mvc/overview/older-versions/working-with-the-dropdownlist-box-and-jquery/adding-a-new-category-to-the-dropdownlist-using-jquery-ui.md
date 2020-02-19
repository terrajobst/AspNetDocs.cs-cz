---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: Přidání nové kategorie do DropDownList pomocí uživatelského rozhraní jQuery | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 3207079ee468232e5f75b081421241c232936baf
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455721"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a>Přidání nové kategorie do ovládacího prvku DropDownList v uživatelském rozhraní jQuery

od [Rick Anderson](https://twitter.com/RickAndMSFT)

Značka HTML `Select` je ideální pro prezentaci seznamu dat pevné kategorie, ale často je potřeba přidat novou kategorii. Předpokládejme, že chceme přidat Žánr "Operait" do kategorií v naší databázi? V této části použijeme uživatelské rozhraní jQuery k přidání dialogového okna, které můžeme použít k přidání nové kategorie. Následující obrázek ukazuje, jak bude uživatelské rozhraní v prohlížeči k dispozici.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

Když uživatel vybere odkaz **Přidat nový žánr** , automaticky otevírané okno vyzve uživatele k zadání nového názvu žánru (a volitelně i popisu). Následující obrázek ukazuje místní dialog **Přidat Žánr** .

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

Při zadání nového názvu žánru a vložení tlačítka **Uložit** dojde k následujícímu:

1. Volání jazyka AJAX odesílá data do metody Create (žánr Controller), která uloží nový žánr do databáze a vrátí nové informace o žánru (název žánru a ID) jako JSON.
2. JavaScript přidá nová data žánru do seznamu SELECT.
3. JavaScript vytvoří nový žánr pro vybranou položku.

   Na následujícím obrázku byl do databáze přidán **Opera** a v rozevíracím seznamu **žánru** byl vybrán. 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

Otevřete soubor *Views\StoreManager\Create.cshtml* a nahraďte kód žánru následujícím kódem:

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

`_ChooseGenre` částečné zobrazení bude obsahovat veškerou logiku pro připojení JavaScriptu a jQuery, která se používá k implementaci funkce Přidat nový žánr. Až kód dokončíme, bude se jednoduše dělat stejně jako uživatelské rozhraní umělce.

V Průzkumník řešení klikněte pravým tlačítkem na složku *Views\StoreManager* a vyberte **Přidat**a pak **Zobrazit**. Do pole **název zobrazení** zadejte `_ChooseGenre` a pak vyberte **Přidat**. Nahraďte kód v souboru *Views\StoreManager\\_ChooseGenre. cshtml* následujícím způsobem:

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

První řádek deklaruje, že předáváme v `Album` jako náš model, přesně stejný příkaz modelu, který byl nalezen v zobrazení vytvořit. Na následujících několika řádcích jsou značky pomocníka **popisku** . Další řádek je pomocné volání **DropDownList** , stejně jako v původním zobrazení pro vytváření. Další řádek přidá odkaz s názvem `Add New Genre`a vytvoří styly jako tlačítko. Řádek obsahující `ValidationMessageFor` se kopíruje přímo ze zobrazení pro vytváření. Následující řádky:

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

Vytvoří skrytý div s ID `genreDialog`. Pomocí jQuery se v tomto div připojíme do dialogového okna **Přidat Žánr** s ID `genreDialog`. Poslední dva značky skriptu obsahují odkazy na soubory JavaScriptu, které budeme používat k implementaci funkce Přidat nový žánr. Soubor */Scripts/chooseGenre.js* je k dispozici v projektu a podíváme se na něj později v tomto kurzu.

Spusťte aplikaci a klikněte na tlačítko **Přidat nový žánr** . V dialogovém okně **Přidat Žánr** zadejte do vstupního pole **název** **Opera** .

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

Klikněte na tlačítko **Uložit**. Volání jazyka AJAX vytvoří kategorii Opera a potom naplní rozevírací seznam pomocí nástroje Opera a nastaví Opera jako vybraný Žánr.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

Zadejte jméno interpreta, název a cenu a pak vyberte tlačítko **vytvořit** . Pokud zadáte cenu menší než $8,99, nové album se zobrazí v horní části zobrazení indexu. Ověřte, že se nová položka alba uložila do databáze.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

Zkuste vytvořit nový žánr s pouze jedním písmenem. Následující kód v souboru *Models\Genre.cs* nastaví minimální a maximální délku názvu žánru.

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

Sestavy ověřování na straně klienta je nutné zadat řetězec o 2 až 20 znacích.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a>Zkoumání toho, jak se do databáze a seznamu pro výběr přidá nový žánr.

Otevřete soubor *Scripts\chooseGenre.js* a Projděte si kód.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

Druhý řádek používá ID `genreDialog` k vytvoření dialogového okna na značce DIV v souboru *\\_ChooseGenre. cshtml pro Views\StoreManager* . Většina pojmenovaných parametrů je vysvětlivekná. Parametr `autoOpen` je nastaven na hodnotu false. Kliknutím na tlačítko **vytvořit Žánr** otevřete dialog explicitně (Tento postup je popsán v tématu). Dialogové okno obsahuje dvě tlačítka, **Uložit** a **Zrušit**. Tlačítko **Storno** zavře dialogové okno. Následující kód ukazuje funkci tlačítko **Uložit** .

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

`var createGenreForm` se vybere z ID `createGenreForm`. ID `createGenreForm` bylo nastaveno v následujícím kódu, který byl nalezen v souboru *Views\Genre\\_CreateGenre. cshtml* .

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

Přetížení pomocné rutiny [HTML. BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) použité v souboru *Views\Genre\\_CreateGenre. cshtml* generuje HTML pomocí atributu Action obsahujícího adresu URL pro odeslání formuláře. Můžete to vidět tak, že v prohlížeči zobrazíte stránku vytvořit album a v prohlížeči vyberete Zobrazit zdroj. Následující kód ukazuje generovaný kód HTML obsahující značku formuláře.

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

Řádek jQuery `$.post` vytvoří volání jazyka AJAX do atributu Action (`/StoreManager/Create`) a předá data z dialogového okna **vytvořit Žánr** . Data se skládají z názvu nového žánru a volitelného popisu. Pokud je volání jazyka AJAX úspěšné, je nový název a hodnota žánru přidány do značky Select a nový žánr je nastaven na vybranou hodnotu. Vzhledem k tomu, že se jedná o dynamicky generované značky, nemůžete zobrazit novou možnost vybrat zobrazením zdroje v prohlížeči. Nový kód HTML můžete zobrazit pomocí vývojářských nástrojů IE 9 F12. Chcete-li zobrazit novou možnost výběru v aplikaci Internet Explorer 9, stiskněte klávesu F12 a spusťte nástroje pro vývojáře F12. Přejděte na stránku vytvořit a přidejte nový žánr, aby byl nový žánr vybrán v seznamu Výběr žánru. V vývojářských nástrojích F12:

1. Vyberte kartu HTML.
2. Stiskněte ikonu aktualizovat.  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. Do vyhledávacího pole zadejte GenreID.
4. Pomocí ikony další   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   přejděte k následující značce SELECT:

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. Rozbalte hodnotu poslední možnosti.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

Následující kód v souboru *Scripts\chooseGenre.js* ukazuje, jak se tlačítko **Přidat nový žánr** připojí k události Click a jak se vytvoří dialogové okno **Přidat nový žánr** .

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

První řádek vytvoří funkci Click připojenou k tlačítku **Přidat nový žánr** . Následující kód ze souboru Views\StoreManager\\_ChooseGenre. cshtml ukazuje, jak se vytvoří tlačítko **Přidat nový žánr** :

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

Metoda load vytvoří a otevře dialog Přidat Žánr a zavolá metodu jQuery `parse`, aby k ověřování klienta došlo na datech zadaných v dialogovém okně.

V této části jste se naučili, jak vytvořit dialog, který se dá použít k přidání nových dat kategorie do seznamu SELECT. Stejný postup můžete použít k vytvoření uživatelského rozhraní pro přidání nového interpreta do seznamu pro výběr interpretu. V tomto kurzu máte přehled o tom, jak pracovat s ovládacím prvkem pro **NÁPOVĚDU HTML**ASP.NET MVC. Další informace o práci s **DropDownList**najdete v části Přidání odkazů níže. Pokud je tento kurz užitečný, dejte nám prosím jistotu.

Rick. Anderson [at] Microsoft. com

### <a name="additional-references"></a>Další odkazy

- [ASP.NET MVC – tento kurz – kaskádové rozevírací seznamy –](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) [radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)
- [Zvolené](https://harvesthq.github.com/chosen/) Modul plug-in JavaScriptu, který podporuje vícenásobné výběry a filtrování.

### <a name="contributors"></a>Spoluautoři

- [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)
- Jean-Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)

### <a name="reviewers"></a>Recenzenti

- Jean-Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)
- Mike Pope
- Dykstra

> [!div class="step-by-step"]
> [Předchozí](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)

---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: Nákupní košík | Microsoft Docs
author: Erikre
description: V této sérii kurzů se seznámíte se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro My...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: 46264a0ab2244cff24761ce94b41722e61e3f426
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614926"
---
# <a name="shopping-cart"></a>Nákupní košík

od [Erik Reitan](https://github.com/Erikre)

[Stáhnout vzorový projekt Wingtip Toys (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [Stáhnout elektronickou knihu (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> V této sérii kurzů se naučíte základy vytváření webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro web. K dispozici je Visual Studio 2013 [projekt se C# zdrojovým kódem](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) , který se doprovází v této sérii kurzů.

Tento kurz popisuje obchodní logiku potřebnou k přidání nákupního košíku do ukázkové ASP.NET webové formuláře Wingtip Toys. Tento kurz sestaví na předchozím kurzu "zobrazení datových položek a podrobností" a je součástí série kurzů Wingtip Toys. Po dokončení tohoto kurzu budou uživatelé ukázkové aplikace moci přidávat, odebírat a upravovat produkty v jejich nákupním košíku.

## <a name="what-youll-learn"></a>Co se naučíte:

1. Jak vytvořit nákupní košík pro webovou aplikaci.
2. Jak uživatelům povolit přidávání položek do nákupního košíku.
3. Postup přidání ovládacího prvku [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction) pro zobrazení podrobností o nákupních košíkech
4. Jak vypočítat a zobrazit celkovou částku objednávky
5. Postup odebrání a aktualizace položek nákupního košíku
6. Zahrnutí čítače nákupního košíku

## <a name="code-features-in-this-tutorial"></a>Funkce kódu v tomto kurzu:

1. Entity Framework Code First
2. Datové poznámky
3. Ovládací prvky dat silného typu
4. Vazby modelu

## <a name="creating-a-shopping-cart"></a>Vytvoření nákupního košíku

Dříve v této sérii kurzů jste přidali stránky a kód pro zobrazení dat produktu z databáze. V tomto kurzu vytvoříte nákupní košík, ve kterém budete spravovat produkty, které si uživatelé chtějí koupit. Uživatelé budou moci procházet a přidávat položky do nákupního košíku i v případě, že nejsou registrováni nebo přihlášeni. Pokud chcete spravovat přístup k nákupnímu košíku, přiřadíte uživatelům jedinečné `ID` pomocí globálně jedinečného identifikátoru (GUID), když uživatel poprvé přistupuje k nákupnímu košíku. Tuto `ID` uložíte pomocí stavu relace ASP.NET.

> [!NOTE] 
> 
> Stav relace ASP.NET je vhodným místem pro ukládání informací specifických pro uživatele, jejichž platnost vyprší poté, co uživatel opustí Web. I když zneužití stavu relace může mít dopad na výkon na větších lokalitách, je vhodné při demonstračních účely využít stav relace. Vzorový projekt Wingtip Toys ukazuje, jak používat stav relace bez externího poskytovatele, kde je stav relace uložen v procesu na webovém serveru, který je hostitelem lokality. U větších webů, které poskytují více instancí aplikace nebo pro lokality, které spouštějí více instancí aplikace na různých serverech, zvažte použití **Windows Azure cache Service**. Tato Cache Service poskytuje distribuovanou službu pro ukládání do mezipaměti, která je externě na webu, a řeší potíže s používáním stavu relace v rámci procesu. Další informace najdete v tématu [použití stavu relace ASP.NET s weby Windows Azure](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider).

### <a name="add-cartitem-as-a-model-class"></a>Přidání CartItem jako třídy modelu

Dříve v této sérii kurzů jste definovali schéma pro kategorii a data produktu vytvořením tříd `Category` a `Product` ve složce *modely* . Nyní přidejte novou třídu k definování schématu pro nákupní košík. Později v tomto kurzu přidáte třídu, která bude zpracovávat přístup k datům `CartItem` tabulce. Tato třída poskytne obchodní logiku pro přidání, odebrání a aktualizaci položek v nákupním košíku.

1. Klikněte pravým tlačítkem na složku *modely* a vyberte **Přidat** -&gt; **Nová položka**. 

    ![Nákupní košík – nová položka](shopping-cart/_static/image1.png)
2. Zobrazí se dialogové okno **Přidat novou položku** . Vyberte **kód**a pak vyberte **Třída**. 

    ![Nákupní košík – dialogové okno Přidat novou položku](shopping-cart/_static/image2.png)
3. Pojmenujte tuto novou třídu *CartItem.cs*.
4. Klikněte na tlačítko **Přidat**.  
   V editoru se zobrazí nový soubor třídy.
5. Nahraďte výchozí kód následujícím kódem:   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

Třída `CartItem` obsahuje schéma, které definuje jednotlivé produkty, které uživatel přidá do nákupního košíku. Tato třída je podobná ostatním třídám schématu, které jste vytvořili dříve v této sérii kurzů. Podle konvence Entity Framework Code First očekává, že bude primární klíč pro `CartItem` tabulka buď `CartItemId`, nebo `ID`. Nicméně kód přepisuje výchozí chování pomocí atributu `[Key]` anotace dat. Atribut `Key` vlastnosti ItemId určuje, že vlastnost `ItemID` je primární klíč.

Vlastnost `CartId` určuje `ID` uživatele, který je přidružen k položce k nákupu. Přidáte kód pro vytvoření tohoto uživatele `ID`, když uživatel přistupuje k nákupnímu košíku. Tento `ID` bude také uložen jako proměnná relace ASP.NET.

### <a name="update-the-product-context"></a>Aktualizace kontextu produktu

Kromě přidání třídy `CartItem` budete muset aktualizovat třídu kontextu databáze, která spravuje třídy entit a která poskytuje přístup k datům databáze. K tomu přidáte nově vytvořenou třídu `CartItem` modelu do `ProductContext` třídy.

1. V **Průzkumník řešení**vyhledejte a otevřete soubor *ProductContext.cs* ve složce *modely* .
2. Do souboru *ProductContext.cs* přidejte zvýrazněný kód následujícím způsobem:  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

Jak bylo zmíněno dříve v této sérii kurzů, kód v souboru *ProductContext.cs* přidá obor názvů `System.Data.Entity`, abyste měli přístup ke všem základním funkcím Entity Framework. Tato funkce zahrnuje možnost dotazování, vkládání, aktualizaci a odstraňování dat pomocí objektů se silnými typy. Třída `ProductContext` přidává přístup k nově přidané třídě `CartItem` modelu.

### <a name="managing-the-shopping-cart-business-logic"></a>Správa obchodní logiky nákupního košíku

V dalším kroku vytvoříte třídu `ShoppingCart` v nové složce *logiky* . Třída `ShoppingCart` zpracovává přístup k datům `CartItem` tabulce. Třída bude také obsahovat obchodní logiku pro přidání, odebrání a aktualizaci položek nákupního košíku.

Logika nákupního košíku, kterou budete přidávat, bude obsahovat funkce pro správu následujících akcí:

1. Přidávání položek do nákupního košíku
2. Odebírání položek z nákupního košíku
3. Získání ID nákupního košíku
4. Načítání položek z nákupního košíku
5. Celkové množství všech položek nákupního košíku
6. Aktualizace dat nákupního košíku

Stránka nákupního košíku (*ShoppingCart. aspx*) a třída nákupního košíku se společně použijí pro přístup k datům nákupního košíku. Na stránce nákupní košík se zobrazí všechny položky, které uživatel přidá do nákupního košíku. Kromě stránky nákupní košíku a třídy vytvoříte stránku (*AddToCart. aspx*) pro přidání produktů do nákupního košíku. Do této stránky také přidáte kód na stránku *ProductList. aspx* a na stránku *ProductDetails. aspx* , která bude obsahovat odkaz na stránku *AddToCart. aspx* , aby uživatel mohl přidat produkty do nákupního košíku.

Následující diagram znázorňuje základní proces, který nastane, když uživatel přidá produkt do nákupního košíku.

![Nákupní košík – přidání do nákupního košíku](shopping-cart/_static/image3.png)

Když uživatel klikne na odkaz **Přidat do košíku** na stránce *ProductList. aspx* nebo na stránce *ProductDetails. aspx* , aplikace přejde na stránku *AddToCart. aspx* a automaticky se zobrazí na stránku *ShoppingCart. aspx* . Na stránce *AddToCart. aspx* se přidá produkt Select do nákupního košíku voláním metody ve třídě ShoppingCart. Na stránce *ShoppingCart. aspx* se zobrazí produkty, které byly přidány do nákupního košíku.

#### <a name="creating-the-shopping-cart-class"></a>Vytvoření třídy nákupního košíku

Třída `ShoppingCart` bude přidána do samostatné složky v aplikaci, takže bude jasné rozlišení mezi modelem (složkou modelů), stránkami (kořenovou složkou) a logikou (složka logiky).

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt **WingtipToys**a vyberte **Přidat**-&gt;**Nová složka**. Pojmenujte novou *logiku*složky.
2. Klikněte pravým tlačítkem na složku *Logic* a pak vyberte **Přidat** -&gt; **Nová položka**.
3. Přidejte nový soubor třídy s názvem *ShoppingCartActions.cs*.
4. Nahraďte výchozí kód následujícím kódem:   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

Metoda `AddToCart` umožňuje, aby jednotlivé produkty byly zahrnuté do nákupního košíku na základě `ID`produktu. Produkt se přidá do košíku, nebo pokud košík již obsahuje položku pro daný produkt, zvýší se množství.

Metoda `GetCartId` vrátí `ID` košíku pro uživatele. `ID` vozíku se používá ke sledování položek, které má uživatel v nákupním košíku. Pokud uživatel nemá existující `ID`košíku, vytvoří se pro ně nový košík `ID`. Pokud je uživatel přihlášený jako registrovaný uživatel, `ID` vozíku se nastaví na své uživatelské jméno. Pokud ale uživatel není přihlášený, `ID` vozíku se nastaví na jedinečnou hodnotu (identifikátor GUID). Identifikátor GUID zajišťuje, že pro každého uživatele je na základě relace vytvořen pouze jeden vozík.

Metoda `GetCartItems` vrátí seznam položek nákupního košíku pro uživatele. Později v tomto kurzu uvidíte, že se vazba modelu používá k zobrazení položek košíku v nákupním košíku pomocí metody `GetCartItems`.

### <a name="creating-the-add-to-cart-functionality"></a>Vytvoření funkce pro přidání do košíku

Jak bylo zmíněno dříve, vytvoříte stránku zpracování s názvem *AddToCart. aspx* , která bude použita k přidání nových produktů do nákupního košíku uživatele. Tato stránka vyvolá metodu `AddToCart` ve třídě `ShoppingCart`, kterou jste právě vytvořili. Na stránce *AddToCart. aspx* se očekává, že se do ní předává produkt `ID`. Tento produkt `ID` bude použit při volání metody `AddToCart` ve třídě `ShoppingCart`.

> [!NOTE] 
> 
> Budete upravovat kód na pozadí (*AddToCart.aspx.cs*) pro tuto stránku, nikoli uživatelské rozhraní stránky (*AddToCart. aspx*).

#### <a name="to-create-the-add-to-cart-functionality"></a>Postup vytvoření funkce přidání do košíku:

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt **WingtipToys**a klikněte na **Přidat** -&gt; **novou položku**.  
   Zobrazí se dialogové okno **Přidat novou položku** .
2. Přidejte standardní novou stránku (webový formulář) do aplikace s názvem *AddToCart. aspx*. 

    ![Nákupní košík – přidat webový formulář](shopping-cart/_static/image4.png)
3. V **Průzkumník řešení**klikněte pravým tlačítkem na stránku *AddToCart. aspx* a pak klikněte na **Zobrazit kód**. Soubor kódu na pozadí *AddToCart.aspx.cs* se otevře v editoru.
4. Nahraďte existující kód v *AddToCart.aspx.cs* kódu za následující:   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

Po načtení stránky *AddToCart. aspx* se produkt `ID` načte z řetězce dotazu. Dále je vytvořena instance třídy nákupního košíku, která se používá k volání metody `AddToCart`, kterou jste přidali dříve v tomto kurzu. Metoda `AddToCart` obsažená v souboru *ShoppingCartActions.cs* obsahuje logiku pro přidání vybraného produktu do nákupního košíku nebo zvýšení množství produktu vybraného produktu. Pokud produkt nebyl přidán do nákupního košíku, produkt se přidá do tabulky `CartItem` databáze. Pokud produkt již byl do nákupního košíku přidán a uživatel přidá další položku stejného produktu, množství produktů se zvýší v `CartItem` tabulce. Nakonec se stránka přesměrovává zpátky na stránku *ShoppingCart. aspx* , kterou přidáte v dalším kroku, kde uživatel uvidí aktualizovaný seznam položek na vozíku.

Jak už jsme uvedli, uživatel `ID` slouží k identifikaci produktů, které jsou přidružené ke konkrétnímu uživateli. Tato `ID` se přidá do řádku v tabulce `CartItem` pokaždé, když uživatel přidá produkt do nákupního košíku.

### <a name="creating-the-shopping-cart-ui"></a>Vytvoření uživatelského rozhraní nákupního košíku

Na stránce *ShoppingCart. aspx* se zobrazí produkty, které uživatel přidal do nákupního košíku. Bude také poskytovat možnost přidávat, odebírat a aktualizovat položky v nákupním košíku.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na **WingtipToys**, klikněte na **Přidat** -&gt; **novou položku**.  
   Zobrazí se dialogové okno **Přidat novou položku** .
2. Přidejte novou stránku (webový formulář), která obsahuje stránku předlohy, výběrem možnosti **webový formulář pomocí stránky předlohy**. Pojmenujte novou stránku *ShoppingCart. aspx*.
3. Vyberte **site. Master** a připojte stránku předlohy k nově vytvořené stránce *aspx* .
4. Na stránce *ShoppingCart. aspx* nahraďte existující kód následujícím kódem:   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

Stránka *ShoppingCart. aspx* obsahuje ovládací prvek **GridView** s názvem `CartList`. Tento ovládací prvek používá vazbu modelu pro svázání dat nákupního košíku z databáze k ovládacímu prvku **GridView** . Když nastavíte vlastnost `ItemType` ovládacího prvku **GridView** , je výraz vazby dat `Item` k dispozici v označení ovládacího prvku a ovládací prvek se bude silného typu. Jak bylo zmíněno dříve v této sérii kurzů, můžete vybrat Podrobnosti objektu `Item` pomocí technologie IntelliSense. Chcete-li nakonfigurovat ovládací prvek data na použití vazby modelu pro výběr dat, nastavte vlastnost `SelectMethod` ovládacího prvku. Ve výše uvedeném kódu nastavíte `SelectMethod` k použití metody GetShoppingCartItems, která vrací seznam objektů `CartItem`. Ovládací prvek **GridView** data volá metodu v příslušnou dobu životního cyklu stránky a automaticky vytvoří vazby vrácených dat. Metoda `GetShoppingCartItems` musí být stále přidána.

#### <a name="retrieving-the-shopping-cart-items"></a>Načítání položek nákupního košíku

Dále přidáte kód do *ShoppingCart.aspx.cs* kódu na pozadí pro načtení a naplnění uživatelského rozhraní nákupního košíku.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na stránku *ShoppingCart. aspx* a pak klikněte na **Zobrazit kód**. Soubor kódu na pozadí *ShoppingCart.aspx.cs* se otevře v editoru.
2. Existující kód nahraďte následujícím kódem:  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

Jak je uvedeno výše, `GridView` ovládací prvek dat volá metodu `GetShoppingCartItems` v příslušnou dobu životního cyklu stránky a automaticky vytvoří vazby vrácených dat. Metoda `GetShoppingCartItems` vytvoří instanci objektu `ShoppingCartActions`. Potom kód používá tuto instanci k vrácení položek na vozíku voláním metody `GetCartItems`.

### <a name="adding-products-to-the-shopping-cart"></a>Přidání produktů do nákupního košíku

Když se zobrazí stránka *ProductList. aspx* nebo *ProductDetails. aspx* , uživatel bude moct produkt přidat do nákupního košíku pomocí odkazu. Když kliknete na odkaz, aplikace přejde na stránku zpracování s názvem *AddToCart. aspx*. Na stránce *AddToCart. aspx* bude volána metoda `AddToCart` ve třídě `ShoppingCart`, kterou jste přidali dříve v tomto kurzu.

Nyní přidáte odkaz **Přidat do košíku** na stránku *ProductList. aspx* a na stránku *ProductDetails. aspx* . Tento odkaz bude zahrnovat produkt `ID` načtený z databáze.

1. V **Průzkumník řešení**vyhledejte a otevřete stránku s názvem *ProductList. aspx*.
2. Přidejte kód zvýrazněný žlutě na stránku *ProductList. aspx* , aby se celá stránka zobrazila takto:  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a>Testování nákupního košíku

Spusťte aplikaci, abyste viděli, jak do nákupního košíku přidat produkty.

1. Stisknutím klávesy **F5** spusťte aplikaci.  
 Poté, co projekt znovu vytvoří databázi, otevře se prohlížeč a zobrazí se stránka *Default. aspx* .
2. V nabídce navigace v kategorii vyberte osobní **automobily** .  
 Zobrazí se stránka *ProductList. aspx* se zobrazením pouze produktů obsažených v kategorii "auta". 

    ![Nákupní košík – automobily](shopping-cart/_static/image5.png)
3. Klikněte na odkaz **Přidat do košíku** vedle prvního produktu uvedeného v seznamu (převoditelné auto).   
 Zobrazí se stránka *ShoppingCart. aspx* zobrazující výběr v nákupním košíku. 

    ![Nákupní košík – košík](shopping-cart/_static/image6.png)
4. Kliknutím na možnost **roviny** z navigační nabídky Kategorie zobrazte další produkty.
5. Klikněte na odkaz **Přidat do košíku** vedle prvního produktu v seznamu.  
 Zobrazí se stránka *ShoppingCart. aspx* s další položkou.
6. Zavřete prohlížeč.

### <a name="calculating-and-displaying-the-order-total"></a>Výpočet a zobrazení součtu objednávky

Kromě přidávání produktů do nákupního košíku přidáte do `ShoppingCart` třídy metodu `GetTotal` a na stránce nákupní košíku se zobrazí celková velikost objednávky.

1. V **Průzkumník řešení**otevřete soubor *ShoppingCartActions.cs* ve složce *Logic* .
2. Přidejte následující metodu `GetTotal` zvýrazněnou žlutou do `ShoppingCart` třídy, aby se třída zobrazila takto:   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

Nejprve metoda `GetTotal` získá ID nákupního košíku pro uživatele. Pak metoda získá součet vozíku vynásobením ceny produktu množstvím produktů pro každý produkt uvedený na vozíku.

> [!NOTE] 
> 
> Výše uvedený kód používá typ s možnou hodnotou null "`int?`". Typy s možnou hodnotou null mohou představovat všechny hodnoty nadřazeného typu a také hodnotu null. Další informace najdete v tématu [použití typů s možnou hodnotou null](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx).

### <a name="modify-the-shopping-cart-display"></a>Upravit zobrazení nákupního košíku

Dále upravíte kód pro stránku *ShoppingCart. aspx* pro volání metody `GetTotal` a po načtení stránky se zobrazí celkem na stránce *ShoppingCart. aspx* .

1. V **Průzkumník řešení**klikněte pravým tlačítkem na stránku *ShoppingCart. aspx* a vyberte **Zobrazit kód**.
2. V souboru *ShoppingCart.aspx.cs* aktualizujte obslužnou rutinu `Page_Load` přidáním následujícího kódu zvýrazněného žlutě:   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

Když se načte stránka *ShoppingCart. aspx* , načte se objekt nákupního košíku a potom se vyplní celková hodnota nákupního košíku voláním metody `GetTotal` třídy `ShoppingCart`. Pokud je nákupní košík prázdný, zobrazí se zpráva s tímto efektem.

### <a name="testing-the-shopping-cart-total"></a>Testování celkových nákupních košíků

Spusťte aplikaci hned, abyste viděli, jak do nákupního košíku nemůžete přidávat jenom produkt, ale můžete zobrazit celkové množství nákupního košíku.

1. Stisknutím klávesy **F5** spusťte aplikaci.  
 V prohlížeči se otevře a zobrazí stránka *Default. aspx* .
2. V nabídce navigace v kategorii vyberte osobní **automobily** .
3. Klikněte na odkaz **Přidat do košíku** vedle prvního produktu.   
 Zobrazí se stránka *ShoppingCart. aspx* s celkovým pořadím. 

    ![Nákupní košík – celková částka na košíku](shopping-cart/_static/image7.png)
4. Přidejte k vozíku některé další produkty (například rovinu).
5. Zobrazí se stránka *ShoppingCart. aspx* s aktualizovaným součtem pro všechny produkty, které jste přidali. 

    ![Nákupní košík – několik produktů](shopping-cart/_static/image8.png)
6. Ukončení spuštěné aplikace zavřením okna prohlížeče.

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a>Přidání tlačítek aktualizace a rezervace do nákupního košíku

Pokud chcete uživatelům dovolit, aby si nákupní košík změnili, přidejte na stránku nákupní košíku tlačítko **aktualizace** a tlačítko pro **rezervaci** . Tlačítko pro **rezervaci** se nepoužívá až do pozdějšího použití v této sérii kurzů.

1. V **Průzkumník řešení**otevřete stránku *ShoppingCart. aspx* v kořenovém adresáři projektu webové aplikace.
2. Chcete-li přidat tlačítko **aktualizace** a tlačítko pro **rezervaci** na stránku *ShoppingCart. aspx* , přidejte kód zvýrazněný žlutě k existujícímu kódu, jak je znázorněno v následujícím kódu:   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

Když uživatel klikne na tlačítko **aktualizovat** , bude volána obslužná rutina události `UpdateBtn_Click`. Tato obslužná rutina události bude volat kód, který přidáte v dalším kroku.

Dále můžete aktualizovat kód obsažený v souboru *ShoppingCart.aspx.cs* tak, aby procházely přes položky košíku, a volat `RemoveItem` a `UpdateItem` metody.

1. V **Průzkumník řešení**otevřete soubor *ShoppingCart.aspx.cs* v kořenovém adresáři projektu webové aplikace.
2. Přidejte následující části kódu zvýrazněné žlutě do souboru *ShoppingCart.aspx.cs* :   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

Když uživatel klikne na stránku *ShoppingCart. aspx* na tlačítko **aktualizovat** , zavolá se metoda UpdateCartItems. Metoda UpdateCartItems načte aktualizované hodnoty pro každou položku v nákupním košíku. Metoda UpdateCartItems pak volá metodu `UpdateShoppingCartDatabase` (přidáno a vysvětlena v dalším kroku), aby buď přidala nebo odebrala položky z nákupního košíku. Po aktualizaci databáze tak, aby odrážela aktualizace nákupního košíku, se ovládací prvek **GridView** aktualizuje na stránce nákupního košíku voláním metody `DataBind` pro **prvek GridView**. Celková částka objednávky na stránce nákupního košíku se také aktualizuje tak, aby odrážela aktualizovaný seznam položek.

### <a name="updating-and-removing-shopping-cart-items"></a>Aktualizace a odebírání položek nákupních košíků

Na stránce *ShoppingCart. aspx* vidíte ovládací prvky, které byly přidány pro aktualizaci množství položky a odebrání položky. Nyní přidejte kód, který zajistí fungování těchto ovládacích prvků.

1. V **Průzkumník řešení**otevřete soubor *ShoppingCartActions.cs* ve složce *Logic* .
2. Přidejte následující kód zvýrazněný žlutě do souboru třídy *ShoppingCartActions.cs* :   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

Metoda `UpdateShoppingCartDatabase` volaná z metody `UpdateCartItems` na stránce *ShoppingCart.aspx.cs* obsahuje logiku pro aktualizaci nebo odebrání položek z nákupního košíku. Metoda `UpdateShoppingCartDatabase` prochází všechny řádky v seznamu nákupních košíků. Pokud byla položka nákupního košíku označena k odebrání nebo je množství menší než jedna, je volána metoda `RemoveItem`. V opačném případě je v případě, že je volána metoda `UpdateItem`, kontrolována položka nákupního košíku. Po odebrání nebo aktualizaci položky nákupního košíku se uloží změny databáze.

Struktura `ShoppingCartUpdates` slouží k uložení všech položek nákupního košíku. Metoda `UpdateShoppingCartDatabase` používá strukturu `ShoppingCartUpdates` k určení, jestli je potřeba aktualizovat nebo odebrat některou z položek.

V dalším kurzu vymažete nákupní košík po zakoupení produktů pomocí metody `EmptyCart`. Zatím ale použijete metodu `GetCount`, kterou jste právě přidali do souboru *ShoppingCartActions.cs* , abyste zjistili, kolik položek je na nákupním košíku.

### <a name="adding-a-shopping-cart-counter"></a>Přidání čítače nákupního košíku

Chcete-li uživateli dovolit zobrazit celkový počet položek v nákupním košíku, přidáte čítač do stránky *Web. Master* . Tento čítač bude také fungovat jako odkaz na nákupní košík.

1. V **Průzkumník řešení**otevřete stránku *Web. Master* .
2. Upravte kód přidáním propojení čítače nákupního košíku, jak je znázorněno žlutě do navigační oblasti, takže se zobrazí takto:  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. Dále aktualizujte kód na pozadí souboru *site.Master.cs* tak, že přidáte kód zvýrazněný žlutě, jak je znázorněno níže:  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

Předtím, než se stránka vykreslí jako HTML, vyvolá se událost `Page_PreRender`. V obslužné rutině `Page_PreRender` je celkový počet nákupních košíků určen voláním metody `GetCount`. Vrácená hodnota je přidána do rozsahu `cartCount` zahrnutého v označení stránky *site. Master* . Značky `<span>` umožňují správné vykreslení vnitřních prvků. Po zobrazení libovolné stránky webu se zobrazí celková hodnota nákupního košíku. Uživatel také může kliknutím na součet nákupního košíku Zobrazit nákupní košík.

## <a name="testing-the-completed-shopping-cart"></a>Testování dokončeného nákupního košíku

Aplikaci teď můžete spustit, abyste viděli, jak můžete přidat, odstranit a aktualizovat položky v nákupním košíku. Celkové náklady na nákupní košík se projeví na všech položkách v nákupním košíku.

1. Stisknutím klávesy **F5** spusťte aplikaci.  
 Prohlížeč otevře a zobrazí stránku *Default. aspx* .
2. V nabídce navigace v kategorii vyberte osobní **automobily** .
3. Klikněte na odkaz **Přidat do košíku** vedle prvního produktu.   
 Zobrazí se stránka *ShoppingCart. aspx* s celkovým pořadím.
4. V nabídce navigace v kategorii vyberte **roviny** .
5. Klikněte na odkaz **Přidat do košíku** vedle prvního produktu.
6. Nastavte množství první položky v nákupním košíku na hodnotu 3 a zaškrtněte políčko **Odebrat položku** u druhé položky.<a id="a"></a>
7. Kliknutím na tlačítko **aktualizovat** aktualizujete stránku nákupní košík a zobrazí se celková objednávka. 

    ![Nákupní košík – aktualizace košíku](shopping-cart/_static/image9.png)

## <a name="summary"></a>Přehled

V tomto kurzu jste vytvořili nákupní košík pro ukázkovou aplikaci Wingtip Toys Web Forms. V tomto kurzu jste použili Entity Framework Code First, datové poznámky, ovládací prvky silného typu dat a vazby modelu.

Nákupní košík podporuje přidávání, odstraňování a aktualizaci položek, které uživatel vybral k nákupu. Kromě implementace funkce nákupního košíku jste zjistili, jak zobrazit položky nákupního košíku v ovládacím prvku **GridView** a vypočítat celkové pořadí.

## <a name="addition-information"></a>Informace o přidání

[Přehled stavu relace ASP.NET](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> [Předchozí](display_data_items_and_details.md)
> [Další](checkout-and-payment-with-paypal.md)

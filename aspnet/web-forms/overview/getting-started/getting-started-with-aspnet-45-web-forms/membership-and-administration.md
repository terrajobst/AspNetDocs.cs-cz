---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: Členství a Správa | Microsoft Docs
author: Erikre
description: V této sérii kurzů se seznámíte se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro My...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: ab00bc90bfc767d06e747be6dfb973245b5aae88
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546737"
---
# <a name="membership-and-administration"></a>Členství a správa

od [Erik Reitan](https://github.com/Erikre)

[Stáhnout vzorový projekt Wingtip Toys (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [Stáhnout elektronickou knihu (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> V této sérii kurzů se naučíte základy vytváření webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro web. K dispozici je Visual Studio 2013 [projekt se C# zdrojovým kódem](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) , který se doprovází v této sérii kurzů.

V tomto kurzu se dozvíte, jak aktualizovat ukázkovou aplikaci Wingtip Toys a přidat vlastní roli a použít ASP.NET Identity. Také se dozvíte, jak implementovat stránku pro správu, ze které může uživatel s vlastní rolí přidávat a odebírat produkty z webu.

[ASP.NET identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md) je systém členství, který se používá k vytvoření webové aplikace v ASP.NET a je k dispozici v ASP.NET 4,5. ASP.NET Identity se používá v šabloně projektu webových formulářů Visual Studio 2013 a také v šablonách pro [ASP.NET MVC](../../../../mvc/index.md), [ASP.NET Web API](../../../../web-api/index.md)a [ASP.NET aplikace s jednou stránkou](../../../../single-page-application/index.md). ASP.NET Identity systém můžete nainstalovat také pomocí nástroje NuGet, když začnete s prázdnou webovou aplikací. V této sérii kurzů ale používáte **webové formuláře**ProjectTemplate, které zahrnují ASP.NET identity systém. ASP.NET Identity usnadňuje integraci dat profilů specifických pro uživatele s daty aplikací. ASP.NET Identity také umožňuje zvolit model trvalosti pro profily uživatelů v aplikaci. Data můžete ukládat do databáze SQL Server nebo do jiného úložiště dat, včetně úložišť dat *NoSQL* , jako jsou například tabulky Windows Azure Storage.

Tento kurz sestaví v předchozím kurzu s názvem "rezervace a platby pomocí služby PayPal" v řadě kurzů Wingtip Toys.

## <a name="what-youll-learn"></a>Naučíte se:

- Jak použít kód k přidání vlastní role a uživatele do aplikace.
- Jak omezit přístup ke složce a stránce pro správu
- Jak poskytnout navigaci pro uživatele, který patří do vlastní role
- Jak použít vazbu modelu k naplnění ovládacího prvku [DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx) pomocí kategorií produktů.
- Postup nahrání souboru do webové aplikace pomocí ovládacího prvku [FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx)
- Jak použít ovládací prvky ověřování k implementaci ověřování vstupu.
- Jak přidávat a odebírat produkty z aplikace

## <a name="these-features-are-included-in-the-tutorial"></a>Tyto funkce jsou zahrnuté v tomto kurzu:

- ASP.NET Identity
- Konfigurace a autorizace
- Vazba modelu
- Nenáročná ověření

Webové formuláře ASP.NET poskytují možnosti členství. Pomocí výchozí šablony máte vestavěnou funkci členství, kterou můžete hned použít při spuštění aplikace. V tomto kurzu se dozvíte, jak pomocí ASP.NET Identity přidat vlastní roli a přiřadit k této roli uživatele. Dozvíte se, jak omezit přístup ke složce pro správu. Přidáte stránku do složky pro správu, která umožňuje uživateli s vlastní rolí přidávat a odebírat produkty a zobrazovat náhled produktu po jeho přidání.

## <a name="adding-a-custom-role"></a>Přidání vlastní role

Pomocí ASP.NET Identity můžete přidat vlastní roli a přiřadit uživatele k této roli pomocí kódu.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na složku *Logic* a vytvořte novou třídu.
2. Pojmenujte novou třídu *RoleActions.cs*.
3. Upravte kód tak, aby se zobrazil následujícím způsobem:  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. V **Průzkumník řešení**otevřete soubor *Global.asax.cs* .
5. Upravte soubor *Global.asax.cs* tak, že přidáte kód zvýrazněný žlutě, aby se zobrazil jako následující:  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. Všimněte si, že `AddUserAndRole` je podtržený červeně. Dvakrát klikněte na kód AddUserAndRole.  
   Písmeno "A" na začátku zvýrazněné metody bude podtrženo.
7. Najeďte myší na písmeno "a" a klikněte na uživatelské rozhraní, které umožňuje vygenerovat zástupnou proceduru metody pro metodu `AddUserAndRole`. 

    ![Členství a Správa – vygenerovat zástupnou proceduru metody](membership-and-administration/_static/image1.png)
8. Klikněte na možnost s názvem:  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. Otevřete soubor *RoleActions.cs* ze složky *Logic* .  
   Do souboru třídy byla přidána metoda `AddUserAndRole`.
10. Upravte soubor *RoleActions.cs* tak, že odeberete `NotImplementedException` a přidáte kód zvýrazněný žlutě, takže se zobrazí takto:  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

Výše uvedený kód nejprve vytvoří kontext databáze pro databázi členství. Databáze členství je také uložena jako soubor *. mdf* ve složce *App\_data* . Tuto databázi budete moci zobrazit po přihlášení prvního uživatele k této webové aplikaci. 

> [!NOTE] 
> 
> Pokud chcete uložit data členství společně s daty produktu, můžete zvážit použití stejného **DbContext** , který jste použili k uložení dat produktu ve výše uvedeném kódu.

 Klíčové slovo *internal* je modifikátor přístupu pro typy (například třídy) a členy typu (například metody nebo vlastnosti). Interní typy nebo členy jsou přístupné pouze v rámci souborů obsažených ve stejném sestavení *(soubor. dll* ). Při sestavování aplikace se vytvoří soubor sestavení *(. dll*), který obsahuje kód, který se spustí při spuštění aplikace. 

Objekt `RoleStore`, který poskytuje správu rolí, je vytvořen na základě kontextu databáze.

> [!NOTE] 
> 
> Všimněte si, že když je objekt `RoleStore` vytvořen, používá obecný typ `IdentityRole`. To znamená, že `RoleStore` může obsahovat pouze objekty `IdentityRole`. Také pomocí obecných typů jsou prostředky v paměti zpracovávány lépe.

Dále je objekt `RoleManager` vytvořen v závislosti na objektu `RoleStore`, který jste právě vytvořili. objekt `RoleManager` zpřístupňuje rozhraní API související s rolí, které lze použít k automatickému uložení změn do `RoleStore`. `RoleManager` může obsahovat pouze objekty `IdentityRole`, protože kód používá `<IdentityRole>` obecný typ.

Voláním metody `RoleExists` určíte, zda je v databázi členství přítomna role "hodnoty CanEdit". Pokud tomu tak není, vytvoříte roli.

Vytvoření objektu `UserManager` se zdá být složitější než ovládací prvek `RoleManager`, ale je téměř stejný. Je právě kódována na jednom řádku, nikoli v několika. Zde je parametr, který předáváte, vytvořen jako nový objekt obsažený v závorkách.

V dalším kroku vytvoříte uživatele "canEditUser" vytvořením nového objektu `ApplicationUser`. Potom, pokud úspěšně vytvoříte uživatele, přidáte uživatele do nové role.

> [!NOTE] 
> 
> Zpracování chyb bude aktualizováno v kurzu "zpracování chyb ASP.NET" dále v této sérii kurzů.

Při příštím spuštění aplikace se uživatel s názvem "canEditUser" přidá jako role s názvem "hodnoty CanEdit" aplikace. Později v tomto kurzu se přihlásíte jako uživatel "canEditUser" a zobrazí se další možnosti, které přidáte během tohoto kurzu. Podrobnosti o rozhraní API o ASP.NET Identity naleznete v [oboru názvů Microsoft. ASPNET. identity](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx). Další podrobnosti o inicializaci ASP.NET Identity systému naleznete v tématu [AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs).

### <a name="restricting-access-to-the-administration-page"></a>Omezení přístupu na stránku správy

Ukázková aplikace Wingtip Toys umožňuje anonymním uživatelům i přihlášeným uživatelům zobrazit a koupit produkty. Přihlášený uživatel, který má vlastní roli "hodnoty CanEdit", však může získat přístup ke stránce s omezeným přístupem, aby mohl přidat nebo odebrat produkty.

#### <a name="add-an-administration-folder-and-page"></a>Přidání složky a stránky pro správu

V dalším kroku vytvoříte složku s názvem *admin* pro uživatele "canEditUser" patřící do vlastní role ukázkové aplikace Wingtip Toys.

1. V **Průzkumník řešení** klikněte pravým tlačítkem myši na název projektu (**Wingtip Toys**) a vyberte **Přidat** -&gt; **Nová složka**.
2. Pojmenujte *správce*nového adresáře.
3. Klikněte pravým tlačítkem na složku *správce* a pak vyberte **Přidat** -&gt; **Nová položka**.   
   Zobrazí se dialogové okno **Přidat novou položku** .
4. Na levé straně vyberte skupinu <strong>Visual C#</strong> -&gt; <strong>Web</strong> Templates. V prostředním seznamu vyberte <strong>webový formulář se stránkou předloha</strong>, pojmenujte ho <em>AdminPage. aspx</em><strong>a pak</strong> vyberte <strong>Přidat</strong>.
5. Vyberte soubor *Web. Master* jako stránku předlohy a pak klikněte na **tlačítko OK**.

#### <a name="add-a-webconfig-file"></a>Přidat soubor Web. config

Přidáním souboru *Web. config* do složky *správce* můžete omezit přístup na stránku obsaženou ve složce.

1. Klikněte pravým tlačítkem na složku *správce* a vyberte **Přidat** -&gt; **Nová položka**.  
   Zobrazí se dialogové okno **Přidat novou položku** .
2. V seznamu C# vizuálních webových šablon vyberte možnost <strong>soubor webové konfigurace</strong>ze seznamu uprostřed, přijměte výchozí název souboru <em>Web. config</em><strong>a pak</strong> vyberte <strong>Přidat</strong>.
3. Nahraďte existující obsah XML v souboru *Web. config* následujícím způsobem:  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

Uložte soubor *Web. config* . Soubor *Web. config* určuje, že přístup k stránce obsažené ve složce pro *správu* může mít jenom uživatel patřící do role "hodnoty CanEdit" aplikace.

### <a name="including-custom-role-navigation"></a>Zahrnutí vlastní navigační role

Chcete-li uživateli vlastní role "hodnoty CanEdit" Povolit navigaci v části Správa aplikace, je nutné přidat odkaz na stránku *Web. Master* . Pouze uživatelé, kteří patří do role "hodnoty CanEdit", budou moci zobrazit odkaz **správce** a získat přístup k části Správa.

1. V Průzkumník řešení vyhledejte a otevřete stránku *Web. Master* .
2. Chcete-li vytvořit odkaz pro uživatele role "hodnoty CanEdit", přidejte kód zvýrazněný žlutě do následujícího neuspořádaného seznamu `<ul>` element tak, aby se seznam zobrazoval takto:  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. Otevřete soubor *site.Master.cs* . Zpřístupněte odkaz pro **správu** pouze uživateli "canEditUser" tím, že přidáte kód zvýrazněný žlutě k obslužné rutině `Page_Load`. Obslužná rutina `Page_Load` se zobrazí takto:   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

Při načtení stránky kód zkontroluje, zda má přihlášený uživatel roli "hodnoty CanEdit". Pokud uživatel patří do role "hodnoty CanEdit", prvek span obsahující odkaz na stránku *AdminPage. aspx* (a následně i odkaz uvnitř rozsahu) je viditelný.

### <a name="enabling-product-administration"></a>Povolení správy produktů

Dosud jste vytvořili roli "hodnoty CanEdit" a Přidali jste uživatele "canEditUser", složku pro správu a stránku pro správu. Nastavili jste přístupová práva ke složce a stránce pro správu a Přidali jste navigační odkaz pro uživatele role "hodnoty CanEdit" do aplikace. V dalším kroku přidáte značku na stránku *AdminPage. aspx* a kód do souboru s kódem na pozadí *AdminPage.aspx.cs* , který umožní uživateli s rolí "hodnoty CanEdit" přidávat a odebírat produkty.

1. V **Průzkumník řešení**otevřete soubor *AdminPage. aspx* ze složky *správce* .
2. Existující značku nahraďte následujícím kódem:  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. Pak otevřete soubor kódu na pozadí *AdminPage.aspx.cs* kliknutím pravým tlačítkem myši na *AdminPage. aspx* a kliknutím na **Zobrazit kód**.
4. Nahraďte existující kód v souboru *AdminPage.aspx.cs* kódu na pozadí následujícím kódem:  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

V kódu, který jste zadali pro soubor *AdminPage.aspx.cs* kódu na pozadí, třída s názvem `AddProducts` provádí skutečnou práci s přidáním produktů do databáze. Tato třída ještě neexistuje, takže ji vytvoříte nyní.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na složku *Logic* a pak vyberte **Přidat** -&gt; **Nová položka**.   
   Zobrazí se dialogové okno **Přidat novou položku** .
2. Na levé straně vyberte skupinu šablon **kódu** &gt; **Visual C#**  -. Pak vyberte **Třída**v prostředním seznamu a pojmenujte ji *AddProducts.cs*.   
   Zobrazí se nový soubor třídy.
3. Existující kód nahraďte následujícím kódem:  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

Stránka *AdminPage. aspx* umožňuje uživatelům patřícím do role "hodnoty CanEdit" přidávat a odebírat produkty. Když se přidá nový produkt, údaje o produktu se ověří a pak se zadají do databáze. Nový produkt je okamžitě k dispozici všem uživatelům webové aplikace.

#### <a name="unobtrusive-validation"></a>Nenáročná ověření

Podrobnosti o produktu, které uživatel poskytuje na stránce *AdminPage. aspx* , se ověřují pomocí ověřovacích ovládacích prvků (`RequiredFieldValidator` a `RegularExpressionValidator`). Tyto ovládací prvky automaticky používají nenáročné ověřování. Nenáročné ověřování umožňuje ovládacím prvkům ověřování používat JavaScript pro logiku ověřování na straně klienta, což znamená, že stránka nevyžaduje, aby se na server ověřila žádná cesta. Ve výchozím nastavení je nenáročná ověřování obsažena v souboru *Web. config* na základě následujícího nastavení konfigurace:

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a>Regulární výrazy

Cena produktu na stránce *AdminPage. aspx* se ověřuje pomocí ovládacího prvku **RegularExpressionValidator** . Tento ovládací prvek ověří, zda hodnota přidruženého vstupního ovládacího prvku (textové pole "AddProductPrice") odpovídá vzoru určenému regulárním výrazem. Regulární výraz je zápis porovnávání se vzorci, který umožňuje rychlé vyhledání a porovnání specifických vzorů znaků. Ovládací prvek **RegularExpressionValidator** obsahuje vlastnost s názvem `ValidationExpression`, která obsahuje regulární výraz používaný k ověření cenového vstupu, jak je znázorněno níže:

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a>Ovládací prvek nahrání souborů

Kromě ovládacích prvků vstupu a ověření jste přidali ovládací prvek **nahrání** do stránky *AdminPage. aspx* . Tento ovládací prvek poskytuje schopnost nahrávat soubory. V tomto případě povolujete nahrávání souborů obrázků. V souboru kódu na pozadí (*AdminPage.aspx.cs*) při kliknutí na `AddProductButton` kód kontroluje vlastnost `HasFile` ovládacího prvku pro **nahrání** souboru. Pokud má ovládací prvek soubor, a pokud je povolený typ souboru (na základě přípony souboru), obrázek se uloží do složky *images* a do složky *Image/miniatury* aplikace.

#### <a name="model-binding"></a>Vazba modelu

Dříve v této sérii kurzů jste použili vazbu modelu k naplnění ovládacího prvku **ListView** , ovládacího prvku **FormsView** , ovládacího prvku **GridView** a ovládacího prvku **prvku detailview** . V tomto kurzu použijete vazbu modelu k naplnění ovládacího prvku **DropDownList** seznamem kategorií produktů.

Kód, který jste přidali do souboru *AdminPage. aspx* , obsahuje ovládací prvek **DropDownList** s názvem `DropDownAddCategory`:

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

Použijte vazbu modelu k naplnění tohoto **ovládacího prvku DropDownList** nastavením atributu `ItemType` a atributu `SelectMethod`. Atribut `ItemType` určuje, zda používáte typ `WingtipToys.Models.Category` při naplňování ovládacího prvku. Tento typ jste na začátku této série kurzů definovali tak, že vytvoříte třídu `Category` (viz níže). Třída `Category` je ve složce *modely* v souboru *Category.cs* .

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

Atribut `SelectMethod` ovládacího prvku **DropDownList** určuje, že použijete metodu `GetCategories` (zobrazenou níže), která je obsažena v souboru kódu na pozadí (*AdminPage.aspx.cs*).

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

Tato metoda určuje, že rozhraní `IQueryable` slouží k vyhodnocení dotazu proti typu `Category`. Vrácená hodnota se používá k naplnění **ovládacího prvkem DropDownList** v kódu stránky (*AdminPage. aspx*).

Text zobrazený pro každou položku v seznamu je určen nastavením atributu `DataTextField`. Atribut `DataTextField` používá `CategoryName` třídy `Category` (zobrazené výše) k zobrazení každé kategorie v ovládacím prvku **DropDownList** . Skutečná hodnota, která je předána, když je vybrána položka v ovládacím prvku **DropDownList** je založena na atributu `DataValueField`. Atribut `DataValueField` je nastaven na `CategoryID`, jak je definováno ve třídě `Category` (zobrazeno výše).

### <a name="how-the-application-will-work"></a>Jak bude aplikace fungovat

Když uživatel, který patří do role "hodnoty CanEdit", přejde na stránku poprvé, `DropDownAddCategory`ovládací prvek **DropDownList** vyplní, jak je popsáno výše. `DropDownRemoveProduct`ovládací prvek **DropDownList** je také vyplněn s produkty, které používají stejný přístup. Uživatel patřící do role "hodnoty CanEdit" vybere typ kategorie a přidá podrobnosti o produktu (**název**, **Popis**, **Cena**a **soubor obrázku**). Když uživatel patřící do role "hodnoty CanEdit" klikne na tlačítko **Přidat produkt** , aktivuje se obslužná rutina události `AddProductButton_Click`. Obslužná rutina události `AddProductButton_Click` umístěná v souboru kódu na pozadí (*AdminPage.aspx.cs*) kontroluje soubor obrázku, aby se ujistil, že odpovídá povoleným typům souborů *(. gif*, *. png*, *. jpeg*nebo *. jpg*). Soubor bitové kopie pak bude uložen do složky ukázkové aplikace Wingtip Toys. V dalším kroku se nový produkt přidá do databáze. Chcete-li dosáhnout přidání nového produktu, je vytvořena nová instance třídy `AddProducts` a pojmenována Products. Třída `AddProducts` obsahuje metodu s názvem `AddProduct`a objekt Products volá tuto metodu pro přidání produktů do databáze.

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

Pokud kód úspěšně přidá nový produkt do databáze, stránka se znovu načte s hodnotou řetězce dotazu `ProductAction=add`.

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

Po opětovném načtení stránky je řetězec dotazu obsažen v adrese URL. Po opětovném načtení stránky může uživatel patřící do role "hodnoty CanEdit" okamžitě zobrazit aktualizace v ovládacích prvcích **DropDownList** na stránce *AdminPage. aspx* . Kromě toho vložením řetězce dotazu s adresou URL může stránka zobrazit zprávu o úspěchu uživateli patřícímu do role "hodnoty CanEdit".

Po opětovném načtení stránky *AdminPage. aspx* se zavolá událost `Page_Load`.

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

Obslužná rutina události `Page_Load` zkontroluje hodnotu řetězce dotazu a určí, zda se má zobrazit zpráva o úspěchu.

## <a name="running-the-application"></a>Spuštění aplikace

Aplikaci teď můžete spustit, abyste viděli, jak můžete přidat, odstranit a aktualizovat položky v nákupním košíku. Celkové náklady na nákupní košík se projeví na všech položkách v nákupním košíku.

1. V Průzkumník řešení stisknutím klávesy **F5** spusťte ukázkovou aplikaci Wingtip Toys.  
   Prohlížeč otevře a zobrazí stránku *Default. aspx* .
2. Klikněte na odkaz **Přihlásit se v** horní části stránky. 

    ![Členství a Správa – odkaz přihlášení](membership-and-administration/_static/image2.png)

   Zobrazí se stránka *Login. aspx* .
3. Použijte následující uživatelské jméno a heslo:  
   Uživatelské jméno: canEditUser@wingtiptoys.com  
   Heslo: PA $ $word 1 

    ![Členství a Správa – přihlašovací stránka](membership-and-administration/_static/image3.png)
4. Klikněte na tlačítko **Přihlásit se v** dolní části stránky.
5. V horní části Další stránky vyberte odkaz **správce** a přejděte na stránku *AdminPage. aspx* . 

    ![Členství a Správa – odkaz pro správu](membership-and-administration/_static/image4.png)
6. Chcete-li otestovat ověřování vstupu, klikněte na tlačítko **Přidat produkt** bez přidání informací o produktu. 

    ![Členství a správa – stránka pro správu](membership-and-administration/_static/image5.png)

   Všimněte si, že se zobrazí požadovaná zpráva pole.
7. Přidejte podrobnosti o novém produktu a pak klikněte na tlačítko **Přidat produkt** . 

    ![Členství a Správa – přidat produkt](membership-and-administration/_static/image6.png)
8. Vyberte možnost **produkty** z horní navigační nabídky k zobrazení nového produktu, který jste přidali. 

    ![Členství a Správa – zobrazit nový produkt](membership-and-administration/_static/image7.png)
9. Kliknutím na odkaz **správce** se vraťte na stránku Správa.
10. V části **odebrat produkt** na stránce vyberte nový produkt, který jste přidali do **DropDownListBox**.
11. Kliknutím na tlačítko **odebrat produkt** odeberte nový produkt z aplikace. 

    ![Členství a Správa – odebrání produktu](membership-and-administration/_static/image8.png)
12. V horní navigační nabídce vyberte **produkty** a potvrďte, že byl produkt odebrán.
13. Klikněte na **Odhlásit** se, aby existoval režim správy.   
    Všimněte si, že horní navigační podokno již nezobrazuje položku nabídky **správce** .

## <a name="summary"></a>Souhrn

V tomto kurzu jste přidali vlastní roli a uživatele, který patří do vlastní role, omezili jste přístup ke složce a stránce pro správu a poskytli jsme navigaci pro uživatele, který patří do vlastní role. Použili jste vazbu modelu k naplnění ovládacího prvku **DropDownList** daty. Implementovali jste ovládací prvky pro **nahrání** a ověřování souborů. Také jste se naučili, jak přidávat a odebírat produkty z databáze. V dalším kurzu se dozvíte, jak implementovat směrování ASP.NET.

## <a name="additional-resources"></a>Další prostředky

[Web. config – autorizační element](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)  
[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[Nasazení zabezpečené aplikace webových formulářů ASP.NET pomocí členství, protokolu OAuth a SQL Database na web Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure – bezplatná zkušební verze](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [Předchozí](checkout-and-payment-with-paypal.md)
> [Další](url-routing.md)

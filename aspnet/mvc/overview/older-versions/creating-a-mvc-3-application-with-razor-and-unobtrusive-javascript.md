---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Vytvoření aplikace MVC 3 se syntaxí Razor a nenápadem JavaScriptu | Microsoft Docs
author: microsoft
description: Ukázková webová aplikace v seznamu uživatelů ukazuje, jak jednoduché je vytvořit ASP.NET aplikace MVC 3 pomocí zobrazovacího modulu Razor. Ukázková aplikace s...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540983"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Vytvoření aplikace MVC 3 se syntaxí Razor a nerušivým JavaScriptem

od [Microsoftu](https://github.com/microsoft)

> Ukázková webová aplikace v seznamu uživatelů ukazuje, jak jednoduché je vytvořit ASP.NET aplikace MVC 3 pomocí zobrazovacího modulu Razor. Ukázková aplikace ukazuje, jak používat nový modul zobrazení Razor s ASP.NET MVC verze 3 a Visual Studio 2010 k vytvoření webu seznam fiktivního uživatele, který obsahuje funkce, jako je vytváření, zobrazování, úpravy a odstraňování uživatelů.
> 
> Tento kurz popisuje kroky, které byly provedeny při sestavování ukázkového seznamu uživatelů aplikace ASP.NET MVC 3. Projekt sady Visual Studio s C# a zdrojový kód VB je k dispozici pro toto téma: [stažení](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114). Pokud máte dotazy k tomuto kurzu, publikujte je prosím na [fóru MVC](https://forums.asp.net/1146.aspx).

## <a name="overview"></a>Přehled

Aplikace, kterou budete sestavovat, je jednoduchý Web seznam uživatelů. Uživatelé mohou zadat, zobrazit a aktualizovat informace o uživateli.

![Ukázkový web](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

Zde si můžete stáhnout VB a C# dokončený [](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)projekt.

## <a name="creating-the-web-application"></a>Vytvoření webové aplikace

Chcete-li spustit kurz, otevřete Visual Studio 2010 a vytvořte nový projekt pomocí šablony *webové aplikace ASP.NET MVC 3* . Pojmenujte aplikaci &quot;Mvc3Razor&quot;.

[![nový projekt MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

V dialogovém okně **Nový projekt ASP.NET MVC 3** vyberte možnost **Internet aplikace**, vyberte modul zobrazení Razor a pak klikněte na tlačítko **OK**.

![Nový projekt ASP.NET MVC 3 – dialog](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

V tomto kurzu nebudete používat poskytovatele členství ASP.NET, takže můžete odstranit všechny soubory spojené s přihlášením a členstvím. V **Průzkumník řešení**odeberte následující soubory a adresáře:

- *Controllers\AccountController*
- *Models\AccountModels*
- *Views\Shared\\_LogOnPartial*
- *Views\Account* (a všechny soubory v tomto adresáři)

![Soln exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

Upravte soubor <em>\_layout. cshtml</em> a nahraďte kód uvnitř elementu `<div>` s názvem `logindisplay` zprávou <em>&quot;</em>přihlášení je zakázané&quot;. Následující příklad ukazuje nový kód:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>Přidání modelu

V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a potom klikněte na **Třída**.

![Nová třída uživatelského MDL](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

Pojmenujte `UserModel`třídy. Obsah souboru *UserModel* nahraďte následujícím kódem:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

Třída `UserModel` představuje uživatele. Každý člen třídy je opatřen poznámkou s [požadovaným](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) atributem z oboru názvů [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) . Atributy v oboru názvů [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) poskytují automatické ověřování na straně klienta a serveru pro webové aplikace.

Otevřete třídu `HomeController` a přidejte direktivu `using`, abyste mohli přistupovat ke třídám `UserModel` a `Users`:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

Hned za `HomeController` deklarací přidejte následující komentář a odkaz na `Users` třídu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

Třída `Users` je zjednodušené úložiště dat v paměti, které použijete v tomto kurzu. V reálné aplikaci byste použili databázi k ukládání informací o uživateli. V následujícím příkladu se zobrazuje několik prvních řádků `HomeController` souboru:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

Sestavte aplikaci tak, aby byl uživatelský model k dispozici průvodci generováním uživatelského rozhraní v dalším kroku.

## <a name="creating-the-default-view"></a>Vytváření výchozího zobrazení

Dalším krokem je přidání metody akce a zobrazení pro zobrazení uživatelů.

Odstraňte existující soubor *Views\Home\Index* . Vytvoří se nový soubor *indexu* pro zobrazení uživatelů.

Ve třídě `HomeController` nahraďte obsah metody `Index` následujícím kódem:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

Klikněte pravým tlačítkem myši do metody `Index` a potom klikněte na tlačítko **Přidat zobrazení**.

![Přidat zobrazení](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

Vyberte možnost **vytvořit zobrazení silného typu** . V **zobrazení třída dat**vyberte **Mvc3Razor. Models. UserModel**. (Pokud nevidíte **Mvc3Razor. Models. UserModel** v poli **Zobrazit data třídy** , je nutné sestavit projekt.) Ujistěte se, že je modul zobrazení nastavený na **Razor**. Nastavte **Zobrazit obsah** na **seznam** a pak klikněte na **Přidat**.

![Přidat zobrazení indexu](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

Nové zobrazení automaticky generuje uživatelská data, která jsou předána do zobrazení `Index`. Prověřte nově vygenerovaný soubor *Views\Home\Index* . Odkazy **vytvořit nové**, **Upravit**, **Podrobnosti**a **Odstranit** nefungují, ale zbytek stránky je funkční. Spusťte stránku. Zobrazí se seznam uživatelů.

![Stránka indexu](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

Otevřete soubor *index. cshtml* a nahraďte `ActionLink` kód pro **Úpravy**, **Podrobnosti**a **odstranění** pomocí následujícího kódu:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

Uživatelské jméno se používá jako ID k vyhledání vybraného záznamu v odkazech **Upravit**, **Podrobnosti**a **Odstranit** .

## <a name="creating-the-details-view"></a>Vytváření zobrazení podrobností

Dalším krokem je přidání metody a zobrazení akce `Details`, aby se zobrazily podrobnosti o uživateli.

![Podrobnosti](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

Do domovského kontroleru přidejte následující metodu `Details`:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

Klikněte pravým tlačítkem myši do metody `Details` a pak vyberte <strong>Přidat zobrazení</strong>. Ověřte, že pole <strong>Třída zobrazení dat</strong> obsahuje <strong>Mvc3Razor. Models. UserModel</strong><em>.</em> Nastavte <strong>zobrazení obsahu</strong> na <strong>Podrobnosti</strong> a potom klikněte na tlačítko <strong>Přidat</strong>.

![Přidat zobrazení podrobností](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

Spusťte aplikaci a vyberte odkaz Podrobnosti. Automatické generování uživatelského rozhraní zobrazuje každou vlastnost v modelu.

![Podrobnosti](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>Vytvoření zobrazení pro úpravy

Do domovského kontroleru přidejte následující metodu `Edit`.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

Přidejte zobrazení jako v předchozích krocích, ale nastavte **Zobrazit obsah** , který chcete **Upravit**.

![Přidat zobrazení pro úpravy](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

Spusťte aplikaci a upravte křestní jméno a příjmení jednoho z uživatelů. Pokud jste porušili jakákoli omezení `DataAnnotation`, která byla použita na třídu `UserModel`, při odeslání formuláře se zobrazí chyby ověřování, které jsou vytvářeny kódem serveru. Pokud například změníte křestní jméno &quot;Ann&quot; na &quot;&quot;, ve formuláři se zobrazí následující chyba:

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

V tomto kurzu považujete uživatelské jméno za primární klíč. Proto nelze změnit vlastnost uživatelského jména. V souboru *Edit. cshtml* hned za příkazem `Html.BeginForm` nastavte uživatelské jméno na skryté pole. Způsobí to, že se vlastnost předává do modelu. Následující fragment kódu ukazuje umístění příkazu `Hidden`:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

Nahraďte `TextBoxFor` a `ValidationMessageFor` označení uživatelského jména pomocí volání `DisplayFor`. Metoda `DisplayFor` zobrazí vlastnost jako element jen pro čtení. Následující příklad ukazuje dokončený kód. Původní volání `TextBoxFor` a `ValidationMessageFor` jsou zakomentovány pomocí znaků Begin-Comment a koncových komentářů Razor (`@* *@`).

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>Povolení ověřování na straně klienta

Chcete-li povolit ověřování na straně klienta v ASP.NET MVC 3, musíte nastavit dva příznaky a musíte zahrnout tři soubory JavaScriptu.

Otevřete soubor *Web. config* aplikace. Ověřte `that ClientValidationEnabled` a `UnobtrusiveJavaScriptEnabled` v nastavení aplikace nastaveny na hodnotu true. Následující fragment v kořenovém souboru *Web. config* zobrazuje správná nastavení:

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

Nastavením `UnobtrusiveJavaScriptEnabled` na true povolíte nenápad AJAX a nebudete moct ověřit klienta. Při použití nenáročného ověřování jsou ověřovací pravidla převedena na atributy HTML5. Názvy atributů HTML5 můžou obsahovat jenom malá písmena, číslice a pomlčky.

Nastavení `ClientValidationEnabled` na true povolí ověřování na straně klienta. Nastavením těchto klíčů v souboru *Web. config* aplikace povolíte ověřování klienta a nenápadný jazyk JavaScript pro celou aplikaci. Tato nastavení můžete povolit nebo zakázat v individuálních zobrazeních nebo v metodách kontroleru pomocí následujícího kódu:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

Také je nutné do vykresleného zobrazení zahrnout několik souborů JavaScriptu. Snadný způsob, jak zahrnout JavaScript do všech zobrazení, je přidat je do souboru *Views\Shared\\_Layout. cshtml* . Nahraďte `<head>` element souboru *\_layout. cshtml* následujícím kódem:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

První dva skripty jQuery jsou hostovány rozhraním Microsoft Ajax Content Delivery Network (CDN). Když využijete Microsoft Ajax CDN, můžete významně vylepšit výkon vašich aplikací při prvním zásahu.

Spusťte aplikaci a klikněte na odkaz Upravit. Zobrazení zdroje stránky v prohlížeči. Zdroj prohlížeče zobrazuje mnoho atributů `data-val` formuláře (pro ověření dat). Když je povolená kontrola klienta a nenáročná technologie JavaScript, vstupní pole s pravidlem ověření klienta obsahují atribut `data-val="true"`, který aktivuje nenáročné ověřování klienta. Například pole `City` v modelu bylo upraveno pomocí [povinného](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) atributu, což vede k zobrazení kódu HTML v následujícím příkladu:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

Pro každé pravidlo ověřování klienta se přidá atribut, který má `data-val-rulename="message"`formuláře. Pomocí příkladu pole `City` uvedeného výše vygeneruje požadované pravidlo ověřování klienta `data-val-required` atribut a zprávu &quot;pole City (město) se vyžaduje&quot;. Spusťte aplikaci, upravte jednoho z nich a zrušte zaškrtnutí pole `City`. Když zaškrtnete pole na kartě, zobrazí se chybová zpráva ověřování na straně klienta.

![Požadováno měst](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

Podobně platí, že pro každý parametr v pravidle ověřování klienta je přidán atribut, který má `data-val-rulename-paramname=paramvalue`formuláře. Například vlastnost `FirstName` je označena atributem [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) a určuje minimální délku 3 a maximální délku 8. Pravidlo ověření dat s názvem `length` má `max` název parametru a hodnotu parametru 8. Následující text zobrazuje kód HTML, který je generován pro pole `FirstName` při úpravě jednoho z uživatelů:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

Další informace o tom, jak neupozornit na ověření klienta, najdete v článku o [nenápadu ověřování klienta v ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) v blogu bradu Wilson.

> [!NOTE]
> V ASP.NET MVC 3 beta je někdy nutné formulář odeslat, aby bylo možné spustit ověřování na straně klienta. To může být pro finální verzi změněno.

## <a name="creating-the-create-view"></a>Vytvoření zobrazení pro vytvoření

Dalším krokem je přidání metody a zobrazení akce `Create`, aby uživatel mohl vytvořit nového uživatele. Do domovského kontroleru přidejte následující metodu `Create`:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

Přidejte zobrazení jako v předchozích krocích, ale nastavte **zobrazení obsahu** na **vytvořit**.

![Create View](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

Spusťte aplikaci, vyberte odkaz **vytvořit** a přidejte nového uživatele. Metoda `Create` automaticky využívá ověřování na straně klienta a serveru. Zkuste zadat uživatelské jméno, které obsahuje prázdné znaky, například &quot;Ben X&quot;. Když zadáte kartu z pole uživatelské jméno, zobrazí se chyba ověřování na straně klienta (`White space is not allowed`).

## <a name="add-the-delete-method"></a>Přidat metodu DELETE

K dokončení tohoto kurzu přidejte do domovského kontroleru následující metodu `Delete`:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

Přidejte zobrazení `Delete` jako v předchozích krocích, nastavením **zobrazení obsahu** pro **odstranění**.

![Odstranit zobrazení](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

Teď máte jednoduchou, ale plně funkční ASP.NET aplikaci MVC 3 s ověřením.

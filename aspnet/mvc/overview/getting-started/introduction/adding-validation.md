---
uid: mvc/overview/getting-started/introduction/adding-validation
title: Přidávání ověřování | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 9f35ca15-e216-4db6-9ebf-24380b0f31b4
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-validation
msc.type: authoredcontent
ms.openlocfilehash: f508d9e38dab5cc4cc44cc5aaa4eae87cf273bd5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615722"
---
# <a name="adding-validation"></a>Přidání ověření

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

V této části přidáte logiku ověřování do modelu `Movie` a zajistěte, aby se ověřovací pravidla vynutila pokaždé, když se uživatel pokusí vytvořit nebo upravit film pomocí aplikace.

## <a name="keeping-things-dry"></a>Udržování věcí v SUŠINě

Jedna z hlavních principy návrhu ASP.NET MVC je [suchá](http://en.wikipedia.org/wiki/Don't_repeat_yourself) (&quot;princip "Neopakuj se"&quot;). ASP.NET MVC vám doporučuje zadat funkce nebo chování jenom jednou a pak je nechat odrážet všude v aplikaci. Tím se sníží množství kódu, který musíte napsat, a kód, který zapíšete méně, je náchylný k chybám a je snazší ho udržovat.

Podpora ověřování poskytovaná ASP.NET MVC a Entity Framework Code First je skvělým příkladem SUCHÉho principu v akci. Můžete deklarativně zadat pravidla ověřování na jednom místě (ve třídě modelu) a pravidla se vynutila všude v aplikaci.

Pojďme se podívat, jak můžete využít tuto podporu ověřování v aplikaci Movie.

## <a name="adding-validation-rules-to-the-movie-model"></a>Přidání ověřovacích pravidel do modelu filmů

Začnete přidáním nějaké ověřovací logiky do třídy `Movie`.

Otevřete soubor *Movie.cs* . Všimněte si, [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) obor názvů neobsahuje `System.Web`. Tato vlastnost poskytuje vestavěnou sadu ověřovacích atributů, které lze deklarativně použít pro libovolnou třídu nebo vlastnost. (Obsahuje také atributy formátování, jako je [datový typ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) , které usnadňují formátování a neposkytují žádné ověřování.)

Teď aktualizujte třídu `Movie`, abyste mohli využívat předdefinované atributy ověřování [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)a [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) . Třídu `Movie` nahraďte následujícím:

[!code-csharp[Main](adding-validation/samples/sample1.cs?highlight=5,13-15,18-19,22-23)]

Atribut [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) nastaví maximální délku řetězce a nastaví toto omezení pro databázi, takže se schéma databáze změní. V **Průzkumníku serveru** klikněte pravým tlačítkem myši na tabulku **filmy** a pak klikněte na **Otevřít definici tabulky**:

![](adding-validation/_static/image1.png)

Na obrázku výše vidíte všechna pole řetězce jsou nastavena na hodnotu [nvarchar (max)](https://technet.microsoft.com/library/ms186939.aspx). K aktualizaci schématu použijeme migrace. Sestavte řešení a otevřete okno **konzoly Správce balíčků** a zadejte následující příkazy:

[!code-console[Main](adding-validation/samples/sample2.cmd)]

Po dokončení tohoto příkazu aplikace Visual Studio otevře soubor třídy definující novou `DbMigration` odvozenou třídu s názvem zadanou (`DataAnnotations`) a v metodě `Up` můžete zobrazit kód, který aktualizuje omezení schématu:

[!code-csharp[Main](adding-validation/samples/sample3.cs)]

Pole `Genre` již nemá hodnotu null (to znamená, že je nutné zadat hodnotu). V poli `Rating` je maximální délka 5 a `Title` maximální délka 60. Minimální délka 3 v `Title` a rozsah `Price` nevytvořil změny schématu.

Prověřte si schéma filmu:

![](adding-validation/_static/image2.png)

Pole řetězců zobrazují omezení pro nové délky a `Genre` již nejsou kontrolována jako Nullable.

Atributy ověřování určují chování, které chcete vyhovět pro vlastnosti modelu, na které se aplikují. Atributy `Required` a `MinimumLength` označují, že vlastnost musí mít hodnotu. ale nic nebrání uživateli v zadání prázdného místa pro splnění tohoto ověření. Atribut [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) slouží k omezení znaků, které lze zadat. Ve výše uvedeném kódu `Genre` a `Rating` musí používat pouze písmena (prázdné znaky, číslice a speciální znaky nejsou povoleny). Atribut [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) omezuje hodnotu na v zadaném rozsahu. Atribut `StringLength` umožňuje nastavit maximální délku řetězcové vlastnosti a volitelně její minimální délku. Typy hodnot (například `decimal, int, float, DateTime`) jsou podstatou požadovány a nepotřebují `Required` atributu.

Code First zajistí, aby se ověřovací pravidla, která zadáte pro třídu modelu, vynutila předtím, než aplikace uloží změny v databázi. Například následující kód vyvolá výjimku [DbEntityValidationException](https://msdn.microsoft.com/library/system.data.entity.validation.dbentityvalidationexception(v=vs.103).aspx) , pokud je volána metoda `SaveChanges`, protože chybí několik požadovaných `Movie` hodnot vlastností:

[!code-csharp[Main](adding-validation/samples/sample4.cs)]

Výše uvedený kód vyvolá následující výjimku:

*Nepodařilo se ověřit jednu nebo více entit. Další podrobnosti najdete ve vlastnosti ' EntityValidationErrors '.*

Automatické vynucení ověřovacích pravidel .NET Framework pomáhá zajistit větší odolnost aplikace. Také zajišťuje, že se nebudete moci zapomenout a neúmyslně ověřit data v databázi.

## <a name="validation-error-ui-in-aspnet-mvc"></a>Uživatelské rozhraní chyby ověřování v ASP.NET MVC

Spusťte aplikaci a přejděte na adresu URL */Movies* .

Kliknutím na odkaz **vytvořit nový** přidejte nový film. Vyplňte formulář s některými neplatnými hodnotami. Jakmile při ověřování na straně klienta jQuery dojde k chybě, zobrazí se chybová zpráva.

![8_validationErrors](adding-validation/_static/image3.png)

> [!NOTE]
> aby bylo možné podporovat ověřování jQuery pro jiné než anglické národní prostředí, které používá čárku (",") pro desetinnou čárku, musíte zahrnout globalizaci NuGet, jak je popsáno dříve v tomto kurzu.

Všimněte si, jak se ve formuláři automaticky používá barva červeného ohraničení, která zvýrazní textová pole obsahující neplatná data a vygenerovala odpovídající chybovou zprávu ověření vedle každé z nich. Chyby se vynutily na straně klienta (pomocí JavaScriptu a jQuery) a na straně serveru (Pokud uživatel má zakázaný JavaScript).

Reálnou výhodou je, že nemusíte změnit jeden řádek kódu ve třídě `MoviesController` nebo v zobrazení *vytvořit. cshtml* , aby bylo možné toto uživatelské rozhraní pro ověřování povolit. Kontroler a zobrazení, které jste vytvořili dříve v tomto kurzu, automaticky vybrala ověřovací pravidla, která jste zadali pomocí atributů ověřování ve vlastnostech třídy `Movie` modelu. Ověření testu pomocí metody `Edit` akce a je použito stejné ověřování.

Data formuláře se neodesílají na server, dokud nedojde k žádným chybám při ověřování na straně klienta. To můžete ověřit tak, že umístíte bod přerušení v metodě HTTP POST, pomocí [nástroje Fiddler](http://fiddler2.com/fiddler2/)nebo [vývojářských nástrojů IE F12](https://msdn.microsoft.com/ie/aa740478).

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Jak probíhá ověřování v metodě vytvořit zobrazení a vytvořit akci

Můžete se setkat s tím, jak se ověřovací uživatelské rozhraní vygenerovalo bez jakýchkoli aktualizací kódu v řadiči nebo zobrazeních. Následující výpis ukazuje, jak `Create` metody ve třídě `MovieController` vypadají jako. Nezměnili jste je, jak jste je vytvořili dříve v tomto kurzu.

[!code-csharp[Main](adding-validation/samples/sample5.cs)]

První metoda (HTTP GET) `Create` akce zobrazí počáteční formulář pro vytvoření. Druhá verze (`[HttpPost]`) zpracovává příspěvek formuláře. Druhá metoda `Create` (verze `HttpPost`) kontroluje `ModelState.IsValid`, zda film obsahuje chyby ověřování. Získání této vlastnosti vyhodnocuje všechny atributy ověřování, které byly u objektu aplikovány. Pokud objekt obsahuje chyby ověřování, metoda `Create` znovu zobrazí formulář. Pokud nejsou k dispozici žádné chyby, metoda uloží nový film do databáze. V našem příkladu filmu není **formulář na straně klienta publikovaný, pokud jsou zjištěny chyby ověření. druhá** **Metoda `Create` nikdy není volána**. Zakážete-li jazyk JavaScript v prohlížeči, bude ověřování klienta zakázáno a metoda HTTP POST `Create` získá `ModelState.IsValid`, aby zkontrolovala, zda film obsahuje chyby ověřování.

Můžete nastavit bod přerušení v metodě `HttpPost Create` a ověřit, zda metoda není nikdy volána, ověřování na straně klienta nebude odesílat data formuláře, pokud jsou zjištěny chyby ověřování. Pokud v prohlížeči zakážete JavaScript, pak formulář odešle s chybami, bude k dispozice bod přerušení. Pořád se vám zobrazí úplné ověření bez JavaScriptu. Následující obrázek ukazuje, jak zakázat JavaScript v aplikaci Internet Explorer.

![](adding-validation/_static/image5.png)

![](adding-validation/_static/image6.png)

Následující obrázek ukazuje, jak zakázat JavaScript v prohlížeči FireFox.

![](adding-validation/_static/image7.png)

Následující obrázek ukazuje, jak zakázat JavaScript v prohlížeči Chrome.

![](adding-validation/_static/image8.png)

Níže je uvedená šablona zobrazení *vytvořit. cshtml* , kterou jste vystavili dříve v tomto kurzu. Používá metody akcí zobrazené výše k zobrazení počátečního formuláře a jeho zobrazení v případě chyby.

[!code-cshtml[Main](adding-validation/samples/sample6.cshtml?highlight=16-17)]

Všimněte si, jak kód používá pomoc `Html.EditorFor` k výstupu prvku `<input>` pro každou vlastnost `Movie`. Vedle této pomocné rutiny je volání pomocné metody `Html.ValidationMessageFor`. Tyto dvě pomocné metody fungují s objektem modelu, který je předán řadičem do zobrazení (v tomto případě objekt `Movie`). Automaticky hledají ověřovací atributy zadané v modelu a zobrazují chybové zprávy podle potřeby.

To je prakticky Skvělé o tomto přístupu, protože řadič ani šablona zobrazení `Create` neví žádné informace o skutečných ověřovacích pravidlech, která se vynucuje, nebo o konkrétních zobrazených chybových zprávách. Ověřovací pravidla a řetězce chyb jsou určeny pouze ve třídě `Movie`. Tato pravidla ověřování se automaticky aplikují na `Edit` zobrazení a na všechny další šablony zobrazení, které můžete vytvořit, když tento model upravíte.

Pokud chcete logiku ověřování změnit později, můžete tak učinit přesně na jednom místě přidáním ověřovacích atributů do modelu (v tomto příkladu třída `movie`). Nemusíte se starat o různé části aplikace, které jsou nekonzistentní s tím, jak se pravidla uplatňují – veškerá logika ověřování bude definovaná na jednom místě a bude se používat všude. Tím se kód neustále čistí a usnadňuje se jeho údržba a vývoj. A to znamená, že budete plně dodržovat zásadu *suchého* .

## <a name="using-datatype-attributes"></a>Použití atributů DataType

Otevřete soubor *Movie.cs* a prověřte třídu `Movie`. Obor názvů [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) poskytuje kromě předdefinované sady ověřovacích atributů také atributy formátování. Pro datum vydání a pole s cenami již jsme použili hodnotu výčtu [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) . Následující kód ukazuje vlastnosti `ReleaseDate` a `Price` s odpovídajícím atributem [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) .

[!code-csharp[Main](adding-validation/samples/sample7.cs)]

Atributy [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) poskytují nápovědu pouze pro modul zobrazení k formátování dat (a zadání atributů, jako je například `<a>` pro adresu URL a `<a href="mailto:EmailAddress.com">` pro e-mail. K ověření formátu dat můžete použít atribut [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) . Atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) se používá k určení datového typu, který je konkrétnější než vnitřní typ databáze, ***nejedná se o atributy ověřování.*** V tomto případě chceme sledovat pouze datum, nikoli datum a čas. [Výčet DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) poskytuje mnoho datových typů, jako je *datum, čas, PhoneNumber, měna, EmailAddress* a další. Atribut `DataType` může také povolit aplikaci automatické poskytování funkcí specifických pro typ. Například odkaz `mailto:` lze vytvořit pro [typ DataType. EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)a selektor data lze zadat pro [typ DataType. Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) v prohlížečích, které podporují [HTML5](http://html5.org/). Atributy [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) emitují atributy [data](http://ejohn.org/blog/html-5-data-attributes/) HTML 5 (vyslovované *datové přerušované*), které mohou prohlížeče HTML 5 pochopit. Atributy [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) neposkytují žádné ověření.

`DataType.Date` neurčuje formát data, které se zobrazí. Ve výchozím nastavení se datové pole zobrazuje v závislosti na výchozích formátech na základě objektu [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)serveru.

Atribut `DisplayFormat` slouží k explicitnímu zadání formátu data:

[!code-csharp[Main](adding-validation/samples/sample8.cs)]

Nastavení `ApplyFormatInEditMode` určuje, že zadané formátování by mělo být použito i v případě, že se hodnota v textovém poli zobrazí pro úpravy. (Pro některá pole (například pro hodnoty měny možná nebudete chtít), nebudete chtít v textovém poli pro úpravy chtít symbol měny.)

Můžete použít atribut [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) sám o sobě, ale obecně je vhodné použít také atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) . Atribut `DataType` předává *sémantiku* dat na rozdíl od způsobu vykreslování na obrazovce a poskytuje následující výhody, které nezískáte pomocí `DisplayFormat`:

- Prohlížeč může povolit funkce HTML5 (například pro zobrazení ovládacího prvku kalendáře, symbolu měny odpovídající národním prostředí, e-mailových odkazů atd.).
- Ve výchozím nastavení bude prohlížeč data vykreslovat pomocí správného formátu na základě vašeho [národního prostředí](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).
- Atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) může MVC povolit, aby vybrali šablonu pravého pole pro vykreslení dat ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) , pokud se používá samostatně, používá šablonu řetězce). Další informace najdete v tématu [šablony ASP.NET MVC 2](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)pro Brad Wilson. (I když je napsaný pro MVC 2, Tento článek se stále vztahuje na aktuální verzi ASP.NET MVC.)

Použijete-li atribut `DataType` s polem datum, je nutné zadat atribut `DisplayFormat` také, aby bylo zajištěno, že pole bude v prohlížečích Chrome správně vykresleno. Další informace najdete v [tomto vlákně StackOverflow](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).

> [!NOTE]
> ověřování jQuery nefunguje s atributem [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) a [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx). Například následující kód bude zobrazovat chybu ověřování na straně klienta, a to i v případě, že je datum v zadaném rozsahu:
> 
> [!code-csharp[Main](adding-validation/samples/sample9.cs)]
> 
> Chcete-li použít atribut [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) s hodnotou [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx), je nutné zakázat ověření data jQuery. Obvykle není dobrým zvykem při kompilování pevných dat ve vašich modelech, takže použití atributu [Range](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) a [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx) se nedoporučuje.

Následující kód ukazuje kombinování atributů na jednom řádku:

[!code-csharp[Main](adding-validation/samples/sample10.cs?highlight=4,6,10,12)]

V další části této série si probereme aplikaci a provedeme některá vylepšení automaticky generovaných `Details` a `Delete`ch metod.

> [!div class="step-by-step"]
> [Předchozí](adding-a-new-field.md)
> [Další](examining-the-details-and-delete-methods.md)

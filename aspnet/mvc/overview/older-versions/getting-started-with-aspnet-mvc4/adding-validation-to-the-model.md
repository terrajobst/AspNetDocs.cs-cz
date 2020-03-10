---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: Přidání ověření do modelu | Microsoft Docs
author: Rick-Anderson
description: 'Poznámka: v této části je k dispozici aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, takže je mnohem jednodušší postupovat a demo...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: c9f6699c5d3500d4c1fcade9252aeb9dd92983da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615029"
---
# <a name="adding-validation-to-the-model"></a>Přidání ověření do modelu

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > K [dispozici je](../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.

V této části přidáte logiku ověřování do modelu `Movie` a zajistěte, aby se ověřovací pravidla vynutila pokaždé, když se uživatel pokusí vytvořit nebo upravit film pomocí aplikace.

## <a name="keeping-things-dry"></a>Udržování věcí v SUŠINě

Jedna z hlavních principy návrhu ASP.NET MVC je SUCHá (&quot;princip "Neopakuj se"&quot;). ASP.NET MVC vám doporučuje zadat funkce nebo chování jenom jednou a pak je nechat odrážet všude v aplikaci. Tím se sníží množství kódu, který musíte napsat, a kód, který zapíšete méně, je náchylný k chybám a je snazší ho udržovat.

Podpora ověřování poskytovaná ASP.NET MVC a Entity Framework Code First je skvělým příkladem SUCHÉho principu v akci. Můžete deklarativně zadat pravidla ověřování na jednom místě (ve třídě modelu) a pravidla se vynutila všude v aplikaci.

Pojďme se podívat, jak můžete využít tuto podporu ověřování v aplikaci Movie.

## <a name="adding-validation-rules-to-the-movie-model"></a>Přidání ověřovacích pravidel do modelu filmů

Začnete přidáním nějaké ověřovací logiky do třídy `Movie`.

Otevřete soubor *Movie.cs* . Přidejte do horní části souboru příkaz `using`, který odkazuje na obor názvů [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) :

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

Všimněte si, že obor názvů neobsahuje `System.Web`. Tato vlastnost poskytuje vestavěnou sadu ověřovacích atributů, které lze deklarativně použít pro libovolnou třídu nebo vlastnost.

Teď aktualizujte třídu `Movie`, abyste mohli využívat předdefinované atributy ověřování [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)a [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) . Použijte následující kód jako příklad, kde použít atributy.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

Spusťte aplikaci a znovu se zobrazí následující chyba běhu:

***Model, který provedl zálohování kontextu ' MovieDBContext ', se od vytvoření databáze změnil. Pokud chcete aktualizovat databázi ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)), zvažte použití migrace Code First.***

K aktualizaci schématu použijeme migrace. Sestavte řešení a otevřete okno **konzoly Správce balíčků** a zadejte následující příkazy:

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

Po dokončení tohoto příkazu aplikace Visual Studio otevře soubor třídy definující novou `DbMigration` odvozenou třídu s názvem, který jste zadali (*AddDataAnnotationsMig*), a v metodě `Up` můžete zobrazit kód, který aktualizuje omezení schématu. Pole `Title` a `Genre` již neumožňují hodnotu null (to znamená, že je nutné zadat hodnotu) a pole `Rating` má maximální délku 5.

Atributy ověřování určují chování, které chcete vyhovět pro vlastnosti modelu, na které se aplikují. Atribut `Required` označuje, že vlastnost musí mít hodnotu. v této ukázce musí mít film hodnotu pro vlastnosti `Title`, `ReleaseDate`, `Genre`a `Price`, aby bylo možné je platné. Atribut `Range` omezuje hodnotu na v zadaném rozsahu. Atribut `StringLength` umožňuje nastavit maximální délku řetězcové vlastnosti a volitelně její minimální délku. Ve výchozím nastavení jsou požadovány vnitřní typy (například `decimal, int, float, DateTime`) a nepotřebují atribut `Required`.

Code First zajistí, aby se ověřovací pravidla, která zadáte pro třídu modelu, vynutila předtím, než aplikace uloží změny v databázi. Například následující kód vyvolá výjimku při volání metody `SaveChanges`, protože chybí několik požadovaných `Movie` hodnot vlastností a cena je nulová (což je mimo platný rozsah).

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

Automatické vynucení ověřovacích pravidel .NET Framework pomáhá zajistit větší odolnost aplikace. Také zajišťuje, že se nebudete moci zapomenout a neúmyslně ověřit data v databázi.

Zde je úplný výpis kódu pro aktualizovaný soubor *Movie.cs* :

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>Uživatelské rozhraní chyby ověřování v ASP.NET MVC

Spusťte aplikaci znovu a přejděte na adresu URL */Movies* .

Kliknutím na odkaz **vytvořit nový** přidejte nový film. Vyplňte formulář s některými neplatnými hodnotami a pak klikněte na tlačítko **vytvořit** .

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> aby bylo možné podporovat ověřování jQuery pro jiné než anglické národní prostředí, které používá čárku (&quot;,&quot;) pro desetinnou čárku, musíte zahrnout *globalizaci. js* a konkrétní soubor *kultury/globalizace. js* (z [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) a jazyk JavaScript pro použití `Globalize.parseFloat`. Následující kód ukazuje úpravy souboru Views\Movies\Edit.cshtml pro práci s &quot;fr-FR&quot; Culture:

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

Všimněte si, jak se ve formuláři automaticky používá barva červeného ohraničení, která zvýrazní textová pole obsahující neplatná data a vygenerovala odpovídající chybovou zprávu ověření vedle každé z nich. Chyby se vynutily na straně klienta (pomocí JavaScriptu a jQuery) a na straně serveru (Pokud uživatel má zakázaný JavaScript).

Reálnou výhodou je, že nemusíte změnit jeden řádek kódu ve třídě `MoviesController` nebo v zobrazení *vytvořit. cshtml* , aby bylo možné toto uživatelské rozhraní pro ověřování povolit. Kontroler a zobrazení, které jste vytvořili dříve v tomto kurzu, automaticky vybrala ověřovací pravidla, která jste zadali pomocí atributů ověřování ve vlastnostech třídy `Movie` modelu.

Je možné, že jste si všimli, že vlastnosti `Title` a `Genre`nejsou vyvynucovány, dokud formulář neodešlete (tlačítko **vytvořit** ), nebo do vstupního pole vložíte text a odebrali jste ho. U pole, které je zpočátku prázdné (například pole v zobrazení pro vytváření) a které má pouze požadovaný atribut a žádné další atributy ověřování, můžete spustit ověření následujícím způsobem:

1. Do pole.
2. Zadejte nějaký text.
3. Karta navýšení kapacity.
4. Tabulátor zpátky do pole.
5. Odeberte text.
6. Karta navýšení kapacity.

Výše uvedená sekvence aktivuje požadované ověření bez toho, aby se aktivovalo tlačítko Odeslat. Stačí, když kliknete na tlačítko Odeslat bez zadání některého z polí, spustí se ověřování na straně klienta. Data formuláře se neodesílají na server, dokud nedojde k žádným chybám při ověřování na straně klienta. To můžete otestovat tak, že umístíte bod přerušení v metodě HTTP POST nebo pomocí nástroje [Fiddler](http://fiddler2.com/fiddler2/) nebo nástrojů pro vývojáře IE 9 [F12](https://msdn.microsoft.com/ie/aa740478).

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Jak probíhá ověřování v metodě vytvořit zobrazení a vytvořit akci

Můžete se setkat s tím, jak se ověřovací uživatelské rozhraní vygenerovalo bez jakýchkoli aktualizací kódu v řadiči nebo zobrazeních. Následující výpis ukazuje, jak `Create` metody ve třídě `MovieController` vypadají jako. Nezměnili jste je, jak jste je vytvořili dříve v tomto kurzu.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

První metoda (HTTP GET) `Create` akce zobrazí počáteční formulář pro vytvoření. Druhá verze (`[HttpPost]`) zpracovává příspěvek formuláře. Druhá metoda `Create` (verze `HttpPost`) volá `ModelState.IsValid`, aby zkontrolovala, zda film obsahuje chyby ověřování. Volání této metody vyhodnotí všechny atributy ověřování, které byly aplikovány na objekt. Pokud objekt obsahuje chyby ověřování, metoda `Create` znovu zobrazí formulář. Pokud nejsou k dispozici žádné chyby, metoda uloží nový film do databáze. V našem příkladu filmu používáme formulář, který se na **straně klienta najde v případě zjištěných chyb ověřování. druhá** **Metoda `Create`nikdy není volána**. Zakážete-li jazyk JavaScript v prohlížeči, bude ověřování klienta zakázáno a metoda HTTP POST `Create` volá `ModelState.IsValid`, aby zkontrolovala, zda film obsahuje chyby ověřování.

Můžete nastavit bod přerušení v metodě `HttpPost Create` a ověřit, zda metoda není nikdy volána, ověřování na straně klienta nebude odesílat data formuláře, pokud jsou zjištěny chyby ověřování. Pokud v prohlížeči zakážete JavaScript, pak formulář odešle s chybami, bude k dispozice bod přerušení. Pořád se vám zobrazí úplné ověření bez JavaScriptu. Následující obrázek ukazuje, jak zakázat JavaScript v aplikaci Internet Explorer.

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

Následující obrázek ukazuje, jak zakázat JavaScript v prohlížeči FireFox.

![](adding-validation-to-the-model/_static/image5.png)

Následující obrázek ukazuje, jak zakázat JavaScript pomocí prohlížeče Chrome.

![](adding-validation-to-the-model/_static/image6.png)

Níže je uvedená šablona zobrazení *vytvořit. cshtml* , kterou jste vystavili dříve v tomto kurzu. Používá metody akcí zobrazené výše k zobrazení počátečního formuláře a jeho zobrazení v případě chyby.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

Všimněte si, jak kód používá pomoc `Html.EditorFor` k výstupu prvku `<input>` pro každou vlastnost `Movie`. Vedle této pomocné rutiny je volání pomocné metody `Html.ValidationMessageFor`. Tyto dvě pomocné metody fungují s objektem modelu, který je předán řadičem do zobrazení (v tomto případě objekt `Movie`). Automaticky hledají ověřovací atributy zadané v modelu a zobrazují chybové zprávy podle potřeby.

To je prakticky Skvělé o tomto přístupu, protože neví, že řadič ani šablona pro vytváření zobrazení neví žádné informace o skutečných ověřovacích pravidlech a o tom, jaké jsou zobrazené chybové zprávy. Ověřovací pravidla a řetězce chyb jsou určeny pouze ve třídě `Movie`. Tato pravidla ověřování se automaticky aplikují na zobrazení pro úpravy a na další šablony zobrazení, které můžete vytvořit, když tento model upravíte.

Pokud chcete logiku ověřování změnit později, můžete tak učinit přesně na jednom místě přidáním ověřovacích atributů do modelu (v tomto příkladu třída `movie`). Nemusíte se starat o různé části aplikace, které jsou nekonzistentní s tím, jak se pravidla uplatňují – veškerá logika ověřování bude definovaná na jednom místě a bude se používat všude. Tím se kód neustále čistí a usnadňuje se jeho údržba a vývoj. A to znamená, že budete plně dodržovat zásadu SUCHÉho.

## <a name="adding-formatting-to-the-movie-model"></a>Přidání formátování do modelu videa

Otevřete soubor *Movie.cs* a prověřte třídu `Movie`. Obor názvů [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) poskytuje kromě předdefinované sady ověřovacích atributů také atributy formátování. Pro datum vydání a pole s cenami již jsme použili hodnotu výčtu [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) . Následující kód ukazuje vlastnosti `ReleaseDate` a `Price` s odpovídajícím atributem [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) .

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

Atributy [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) nejsou ověřovány, používají se k oznámení, že zobrazovací modul vykresluje kód HTML. V předchozím příkladu atribut `DataType.Date` zobrazuje data videa pouze jako data, a to bez času. Například následující atributy [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) neověřují formát dat:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

Výše uvedené atributy poskytují nápovědu pro modul zobrazení k formátování dat (a zadání atributů, jako je například &lt;&gt; pro adresu URL a &lt;href =&quot;mailto:EmailAddress. com&quot;&gt; pro e-mail. K ověření formátu dat můžete použít atribut [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) .

Alternativním přístupem k použití atributů `DataType` můžete explicitně nastavit [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) hodnotu. Následující kód ukazuje vlastnost datum vydání s řetězcem formátu data (konkrétně &quot;d&quot;). Pomocí tohoto nastavení určíte, že jako součást data vydání nechcete čas.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

Kompletní `Movie` třída je uvedena níže.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

Spusťte aplikaci a přejděte k řadiči `Movies`. Datum a cena vydané verze jsou v tomto formátu probíhají. Následující obrázek ukazuje datum a cenu vydání pomocí &quot;fr-FR&quot; jako jazykovou verzi.

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

Následující obrázek ukazuje stejná data zobrazená s výchozí jazykovou verzí (angličtina US).

![](adding-validation-to-the-model/_static/image8.png)

V další části této série si probereme aplikaci a provedeme některá vylepšení automaticky generovaných `Details` a `Delete`ch metod.

> [!div class="step-by-step"]
> [Předchozí](adding-a-new-field-to-the-movie-model-and-table.md)
> [Další](examining-the-details-and-delete-methods.md)

---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: Vazba parametrů ve webovém rozhraní API ASP.NET – ASP.NET 4. x
author: MikeWasson
description: Popisuje, jak rozhraní Web API váže parametry a jak přizpůsobit proces vazby v ASP.NET 4. x.
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 032368f94ce32cf6231458649e8fdd42bee685e9
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519255"
---
# <a name="parameter-binding-in-aspnet-web-api"></a>Vazba parametrů ve webovém rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

[!INCLUDE[](~/includes/coreWebAPI.md)]

Tento článek popisuje, jak rozhraní Web API váže parametry a jak můžete přizpůsobit proces vazby. Když webové rozhraní API volá metodu na řadiči, musí nastavit hodnoty pro parametry, což je proces s názvem *vazba*.

Ve výchozím nastavení používá webové rozhraní API následující pravidla pro svázání parametrů:

- Pokud je parametr "jednoduchý" typ, webové rozhraní API se pokusí získat hodnotu z identifikátoru URI. Mezi jednoduché typy patří [primitivní typy](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) rozhraní .NET (**int**, **bool**, **Double**a tak dále), plus **TimeSpan**, **DateTime**, **GUID**, **Decimal**a **String**a *navíc* libovolný typ s konvertorem typu, který může být převeden z řetězce. (Další informace o převaděčích typů později.)
- Pro komplexní typy se webové rozhraní API pokusí přečíst hodnotu z těla zprávy pomocí [formátovacího modulu typu média](media-formatters.md).

Příkladem je příklad typické metody řadiče webového rozhraní API:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

Parametr *ID* je &quot;jednoduchý&quot; typ, takže se webové rozhraní API pokusí získat hodnotu z identifikátoru URI požadavku. Parametr *Item* je komplexní typ, takže webové rozhraní API používá ke čtení hodnoty z textu žádosti formátovací modul typu Media.

Pokud chcete získat hodnotu z identifikátoru URI, webové rozhraní API bude hledat v řetězci směrování dat a v řetězci dotazu identifikátoru URI. Data trasy se naplní, když systém směrování analyzuje identifikátor URI a odpovídá na trasu. Další informace najdete v tématu [Směrování a výběr akcí](../web-api-routing-and-actions/routing-and-action-selection.md).

Ve zbývající části tohoto článku si ukážeme, jak můžete přizpůsobit proces vazby modelu. U komplexních typů však zvažte použití formátovacích formátovacích typů médií, kdykoli je to možné. Klíčovým principem protokolu HTTP je odeslání prostředků do těla zprávy pomocí vyjednávání obsahu pro určení reprezentace prostředku. Formátovací moduly typu média byly navrženy pro přesně tento účel.

## <a name="using-fromuri"></a>Použití [FromUri]

Chcete-li vynutit, aby webové rozhraní API četlo komplexní typ z identifikátoru URI, přidejte do parametru atribut **[FromUri]** . Následující příklad definuje typ `GeoPoint` společně s metodou kontroléru, která získá `GeoPoint` z identifikátoru URI.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

Klient může do řetězce dotazu umístit hodnoty zeměpisné šířky a délky a webové rozhraní API je bude používat k sestavení `GeoPoint`. Příklad:

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a>Použití [FromBody]

Chcete-li vynutit, aby webové rozhraní API četlo jednoduchý typ z těla žádosti, přidejte do parametru atribut **[FromBody]** :

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

V tomto příkladu webové rozhraní API použije ke čtení hodnoty *názvu* z textu žádosti formátovací modul typu Media. Tady je příklad žádosti klienta.

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

Když parametr obsahuje [FromBody], webové rozhraní API použije hlavičku Content-Type k výběru formátovacího modulu. V tomto příkladu je typ obsahu &quot;Application/JSON&quot; a tělo požadavku je nezpracovaný řetězec JSON (ne objekt JSON).

Čtení z textu zprávy může mít maximálně jeden parametr. Takže to nebude fungovat:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

Důvodem pro toto pravidlo je, že text požadavku může být uložený v nebufferovém datovém proudu, který se dá číst jenom jednou.

## <a name="type-converters"></a>Převaděče typů

Webové rozhraní API můžete považovat za jednoduchý typ (takže se webové rozhraní API pokusí vytvořit vazby z identifikátoru URI) vytvořením **třídy TypeConverter** a zadáním převodu řetězce.

Následující kód ukazuje `GeoPoint` třídu reprezentující zeměpisný bod a **třídu TypeConverter** , která je převedena z řetězců na `GeoPoint` instance. Třída `GeoPoint` je upravena pomocí atributu **[TypeConverter]** pro určení konvertoru typu. (Tento příklad byl nechte inspirovat na blogovém příspěvku Jan Stallion, [jak vytvořit vazby k vlastním objektům v podpisech akcí v MVC/WebApi](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

Nyní bude webové rozhraní API zacházet `GeoPoint` jako jednoduchý typ, což znamená, že se pokusí navazovat `GeoPoint` parametry z identifikátoru URI. Do parametru není nutné zahrnout **[FromUri]** .

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

Klient může metodu vyvolat pomocí identifikátoru URI, například:

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a>Pořadače modelů

Pružnější možnost než konvertor typu je vytvoření vlastního pořadače modelů. Pomocí pořadače modelů máte přístup k takovým akcím, jako je požadavek HTTP, popis akce a nezpracované hodnoty z dat směrování.

Chcete-li vytvořit pořadač modelů, implementujte rozhraní **IModelBinder** . Toto rozhraní definuje jedinou metodu **BindModel**:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

Tady je modelový pořadač pro `GeoPoint` objekty.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

Pořadač modelů získá nezpracované vstupní hodnoty od *poskytovatele hodnot*. Tento návrh odděluje dvě různé funkce:

- Zprostředkovatel hodnoty převezme požadavek HTTP a naplní slovník párů klíč-hodnota.
- Pořadač modelů používá tento slovník k naplnění modelu.

Výchozí zprostředkovatel hodnoty ve webovém rozhraní API získává hodnoty z dat směrování a řetězce dotazu. Například pokud je identifikátor URI `http://localhost/api/values/1?location=48,-122`, zprostředkovatel hodnoty vytvoří následující páry klíč-hodnota:

- id = &quot;1&quot;
- Location = &quot;48 122&quot;

(Předpokládáme výchozí šablonu směrování, která je &quot;API/{Controller}/{ID}&quot;.)

Název parametru, který se má vytvořit, je uložený ve vlastnosti **ModelBindingContext. model** . Pořadač modelů vyhledá klíč s touto hodnotou ve slovníku. Pokud hodnota existuje a je možné ji převést na `GeoPoint`, pořadač modelů přiřadí vázanou hodnotu k vlastnosti **ModelBindingContext. model** .

Všimněte si, že pořadač modelů není omezený na jednoduchý převod typu. V tomto příkladu pořadač modelů nejprve vyhledá tabulku známých umístění a pokud se to nepovede, používá převod typu.

**Nastavení pořadače modelů**

Existuje několik způsobů, jak nastavit pořadač modelů. Nejprve můžete k parametru přidat atribut **[ModelBinder]** .

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

K typu můžete také přidat atribut **[ModelBinder]** . Webové rozhraní API bude používat zadaný modelový pořadač pro všechny parametry tohoto typu.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

Nakonec můžete přidat poskytovatele modelového pořadače do **HttpConfiguration**. Poskytovatel pořadače modelů je jednoduše třída továrny, která vytváří pořadač modelů. Zprostředkovatele můžete vytvořit odvozením z třídy [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) . Pokud však pořadač modelů zpracovává jeden typ, je snazší použít vestavěný **SimpleModelBinderProvider**, která je navržena pro tento účel. Následující kód ukazuje, jak to provést.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

U poskytovatele vázání modelů stále potřebujete přidat do parametru atribut **[ModelBinder]** , aby bylo možné sdělit webovému rozhraní API, že by měl používat pořadač modelů a nikoli formátování mediálního typu. Nyní ale není nutné zadávat typ pořadače modelů v atributu:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a>Zprostředkovatelé hodnot

Uvedli jsem, že pořadač modelů Získá hodnoty od poskytovatele hodnot. Chcete-li napsat vlastního zprostředkovatele hodnoty, implementujte rozhraní **IValueProvider** . Tady je příklad, který načte hodnoty z souborů cookie v žádosti:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

Také je nutné vytvořit továrnu poskytovatele hodnot odvozenou od třídy **ValueProviderFactory** .

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

Přidejte objekt pro vytváření zprostředkovatele hodnoty do **HttpConfiguration** následujícím způsobem.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

Webové rozhraní API vytvoří všechny poskytovatele hodnot, takže když pořadač modelu volá **ValueProvider. GetValue**, modelový pořadač obdrží hodnotu od prvního poskytovatele hodnoty, který je schopný ho vytvořit.

Alternativně můžete nastavit objekt pro vytváření zprostředkovatele hodnoty na úrovni parametru pomocí atributu **ValueProvider** následujícím způsobem:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

To oznamuje webovému rozhraní API použití vazby modelu se zadaným objektem pro vytváření zprostředkovatelů hodnot a nepoužívá žádné jiné registrované zprostředkovatele registrovaných hodnot.

## <a name="httpparameterbinding"></a>HttpParameterBinding

Pořadače modelů jsou konkrétní instancí obecnější mechanismu. Pokud se podíváte na atribut **[ModelBinder]** , uvidíte, že je odvozen z abstraktní třídy **ParameterBindingAttribute** . Tato třída definuje jedinou metodu **GetBinding**, která vrací objekt **HttpParameterBinding** :

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

**HttpParameterBinding** zodpovídá za vazbu parametru na hodnotu. V případě **[ModelBinder]** vrátí atribut implementaci **HttpParameterBinding** , která používá **IModelBinder** k provedení skutečné vazby. Můžete také implementovat vlastní **HttpParameterBinding**.

Předpokládejme například, že chcete získat značky ETag z `if-match` a `if-none-match` hlavičky v požadavku. Začneme definováním třídy, která bude představovat značky ETag.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

Také definujeme výčet, který označuje, jestli se má získat ETag z hlavičky `if-match` nebo z hlavičky `if-none-match`.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

Zde je **HttpParameterBinding** , který získá značku ETag z požadované hlavičky a váže ji k parametru typu ETag:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

Metoda **ExecuteBindingAsync** provede vazbu. V rámci této metody přidejte hodnotu vázaného parametru do **ActionArgument** slovníku v **HttpActionContext**.

> [!NOTE]
> Pokud vaše metoda **ExecuteBindingAsync** přečte tělo zprávy s požadavkem, přepište vlastnost **WillReadBody** na hodnotu true. Text požadavku může být datový proud bez vyrovnávací paměti, který se dá číst jenom jednou, takže webové rozhraní API vynutilo pravidlo, které může přečíst tělo zprávy na maximálně jedné vazbě.

Chcete-li použít vlastní **HttpParameterBinding**, můžete definovat atribut, který je odvozen z **ParameterBindingAttribute**. Pro `ETagParameterBinding`definujeme dva atributy, jednu pro `if-match` záhlaví a jednu pro `if-none-match` hlaviček. Obě jsou odvozeny od abstraktní základní třídy.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

Zde je metoda kontroleru, která používá atribut `[IfNoneMatch]`.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

Kromě **ParameterBindingAttribute**existuje další zavěšení pro přidání vlastní **HttpParameterBinding**. V objektu **HttpConfiguration** je vlastnost **ParameterBindingRules** kolekcí anonymních funkcí typu (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**). Například můžete přidat pravidlo, které jakýkoli parametr ETag v metodě GET používá `ETagParameterBinding` s `if-none-match`:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

Funkce by měla vracet `null` pro parametry, kde vazba není k dispozici.

## <a name="iactionvaluebinder"></a>IActionValueBinder

Celý proces vázání parametrů je řízen službou, kterou může připojit **IActionValueBinder**. Výchozí implementace **IActionValueBinder** provádí následující akce:

1. Vyhledejte v parametru **ParameterBindingAttribute** . To zahrnuje **[FromBody]** , **[FromUri]** a **[ModelBinder]** , nebo vlastní atributy.
2. V opačném případě vyhledejte **HttpConfiguration. ParameterBindingRules** pro funkci, která vrací **HttpParameterBinding**s hodnotou jinou než null.
3. Jinak použijte výchozí pravidla, která jsme popsali dříve. 

    - Pokud je typ parametru "jednoduchý" nebo má konvertor typu, vazba z identifikátoru URI. Jedná se o ekvivalent pro vložení atributu **[FromUri]** v parametru.
    - V opačném případě se pokuste načíst parametr z textu zprávy. Jedná se o ekvivalent umístění **[FromBody]** v parametru.

Pokud jste chtěli, můžete nahradit celou službu **IActionValueBinder** vlastní implementací.

## <a name="additional-resources"></a>Další materiály a zdroje informací

[Ukázka vazby vlastního parametru](http://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

Jan kout zapsal dobrý seriál blogových příspěvků o vazbě parametru webového rozhraní API:

- [Způsob vazby parametrů webového rozhraní API](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [Vazba parametrů stylu MVC pro webové rozhraní API](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [Vytvoření vazby na vlastní objekty v podpisech akcí v MVC nebo webovém rozhraní API](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [Postup vytvoření vlastního zprostředkovatele hodnoty ve webovém rozhraní API](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [Vazba parametrů webového rozhraní API v digestoři](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)

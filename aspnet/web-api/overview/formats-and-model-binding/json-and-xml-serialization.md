---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: Serializace JSON a XML ve ASP.NET Web API – ASP.NET 4. x
author: MikeWasson
description: Popisuje formátovací moduly JSON a XML ve webovém rozhraní API ASP.NET pro ASP.NET 4. x.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 00fa07f00eabf7e6c883c5e9ceaf9a38a8f49605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557468"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>JSON a serializace XML ve webovém rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Tento článek popisuje formátování JSON a XML ve webovém rozhraní API ASP.NET.

Ve webovém rozhraní API ASP.NET je *modul formátování mediálního typu* objekt, který může:

- Čtení objektů CLR z těla zprávy HTTP
- Zápis objektů CLR do těla zprávy HTTP

Webové rozhraní API poskytuje formátovací moduly typu média pro JSON i XML. Rozhraní vloží tyto formátovací moduly do kanálu ve výchozím nastavení. Klienti můžou v hlavičce Accept požadavku HTTP požadovat buď JSON, nebo XML.

## <a name="contents"></a>Obsah

- [Formátovací modul typu médium JSON](#json_media_type_formatter)

    - [Vlastnosti jen pro čtení](#json_readonly)
    - [Datech](#json_dates)
    - [Odsazení](#json_indenting)
    - [Ve stylu CamelCase velká a malá písmena](#json_camelcasing)
    - [Anonymní a slabě typované objekty](#json_anon)
- [Formátovací modul XML typu média](#xml_media_type_formatter)

    - [Vlastnosti jen pro čtení](#xml_readonly)
    - [Datech](#xml_dates)
    - [Odsazení](#xml_indenting)
    - [Nastavení serializátorů XML pro jednotlivé typy](#xml_pertype)
- [Odebrání formátovacího modulu JSON nebo XML](#removing_the_json_or_xml_formatter)
- [Zpracování cyklických odkazů na objekty](#handling_circular_object_references)
- [Testování serializace objektu](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>Formátovací modul typu médium JSON

Formátování JSON je poskytováno třídou **JsonMediaTypeFormatter** . Ve výchozím nastavení používá **JsonMediaTypeFormatter** k provedení serializaci knihovnu [JSON.NET](https://github.com/JamesNK/Newtonsoft.Json) . Json.NET je open source projekt třetí strany.

Pokud dáváte přednost, můžete třídu **JsonMediaTypeFormatter** nakonfigurovat tak, aby používala **DataContractJsonSerializer** namísto JSON.NET. Provedete to tak, že nastavíte vlastnost **UseDataContractJsonSerializer** na **hodnotu true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>Serializace JSON

Tato část popisuje některá konkrétní chování formátovacího modulu JSON s použitím výchozího serializátoru [JSON.NET](https://github.com/JamesNK/Newtonsoft.Json) . Nejedná se o komplexní dokumentaci knihovny Json.NET. Další informace najdete v [dokumentaci k JSON.NET](http://james.newtonking.com/projects/json/help/).

#### <a name="what-gets-serialized"></a>Co získám serializaci?

Ve výchozím nastavení jsou všechny veřejné vlastnosti a pole zahrnuté v serializovaném formátu JSON. Chcete-li vypustit vlastnost nebo pole, seupravte je pomocí atributu **JsonIgnore** .

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

Pokud dáváte přednost &quot;výslovný&quot; přístup, seřazením třídy pomocí atributu **DataContract** . Pokud je tento atribut přítomen, jsou členy ignorovány, pokud nemají **DataMember**. Můžete také použít **DataMember** k serializaci privátních členů.

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>Vlastnosti jen pro čtení

Ve výchozím nastavení jsou serializovány vlastnosti jen pro čtení.

<a id="json_dates"></a>
### <a name="dates"></a>Kalendářní data

Ve výchozím nastavení Json.NET zapisuje data ve formátu [ISO 8601](http://www.w3.org/TR/NOTE-datetime) . Data v UTC (koordinovaný světový čas) se napíší příponou "Z". Kalendářní data v místním čase zahrnují posun časového pásma. Příklad:

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

Ve výchozím nastavení Json.NET zachovává časové pásmo. To můžete přepsat nastavením vlastnosti DateTimeZoneHandling:

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

Pokud raději použijete [formát data JSON od společnosti Microsoft](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) místo ISO 8601, nastavte vlastnost **DateFormatHandling** v nastavení serializátoru:

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>Odsazení

Pro zápis odsazeného JSON nastavte nastavení **formátování** na **formátování. odsazené**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>Ve stylu CamelCase velká a malá písmena

Pro zápis názvů vlastností JSON s ve stylu camelcasemi velkými písmeny bez změny datového modelu nastavte **CamelCasePropertyNamesContractResolver** na serializátoru:

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>Anonymní a slabě typované objekty

Metoda akce může vracet anonymní objekt a serializovat ho do formátu JSON. Příklad:

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

Tělo zprávy odpovědi bude obsahovat následující kód JSON:

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

Pokud vaše webové rozhraní API obdrží volně strukturované objekty JSON od klientů, můžete text žádosti deserializovat do typu **Newtonsoft. JSON. Linq. JObject** .

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

Je ale obvykle lepší používat datové objekty silného typu. Pak nemusíte data analyzovat sami a získáte výhody ověřování modelu.

Serializátor XML nepodporuje anonymní typy nebo **JObject** instance. Pokud používáte tyto funkce pro data JSON, měli byste z kanálu odebrat formátovací modul XML, jak je popsáno dále v tomto článku.

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>Formátovací modul XML typu média

Formátování XML je zajištěno třídou **XmlMediaTypeFormatter** . Ve výchozím nastavení **XmlMediaTypeFormatter** používá třídu **DataContractSerializer** k provedení serializace.

Pokud chcete, můžete **XmlMediaTypeFormatter** nakonfigurovat tak, aby používal **XmlSerializer** namísto **DataContractSerializer**. Provedete to tak, že nastavíte vlastnost **useXmlSerializer** na **hodnotu true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

Třída **XmlSerializer** podporuje užší sadu typů než **DataContractSerializer**, ale poskytuje větší kontrolu nad výsledným XML. Pokud potřebujete odpovídat existujícímu schématu XML, zvažte použití **XmlSerializer** .

### <a name="xml-serialization"></a>Serializace XML

Tato část popisuje některá konkrétní chování formátovacího modulu XML s použitím výchozí třídy **DataContractSerializer**.

Ve výchozím nastavení se třída DataContractSerializer chová takto:

- Všechny veřejné vlastnosti pro čtení i zápis a pole jsou serializovány. Chcete-li vypustit vlastnost nebo pole, seupravte je pomocí atributu **IgnoreDataMember** .
- Soukromé a chráněné členy nejsou serializovány.
- Vlastnosti jen pro čtení nejsou serializovány. (Obsah vlastnosti kolekce jen pro čtení je však serializován.)
- Názvy tříd a členů jsou zapsány v XML přesně tak, jak jsou uvedeny v deklaraci třídy.
- Použije se výchozí obor názvů XML.

Pokud potřebujete větší kontrolu nad serializací, můžete třídu vytřídit pomocí atributu **DataContract** . Pokud je tento atribut přítomen, třída je serializována následujícím způsobem:

- &quot;opt&quot; přístup: vlastnosti a pole nejsou ve výchozím nastavení serializovány. Chcete-li serializovat vlastnost nebo pole, seupravte je pomocí atributu **DataMember** .
- Chcete-li serializovat soukromý nebo chráněný člen, jej seupravte pomocí atributu **DataMember** .
- Vlastnosti jen pro čtení nejsou serializovány.
- Chcete-li změnit způsob, jakým se v XML zobrazí název třídy, nastavte parametr *Name* v atributu **DataContract** .
- Chcete-li změnit způsob, jakým se název člena zobrazí v XML, nastavte parametr *Name* v atributu **DataMember** .
- Chcete-li změnit obor názvů XML, nastavte parametr *Namespace* ve třídě **DataContract** .

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>Vlastnosti jen pro čtení

Vlastnosti jen pro čtení nejsou serializovány. Pokud má vlastnost jen pro čtení záložní privátní pole, můžete označit soukromé pole atributem **DataMember** . Tento přístup vyžaduje pro třídu atribut **DataContract** .

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>Kalendářní data

Data jsou zapsána ve formátu ISO 8601. Například &quot;2012-05-23T20:21:37.9116538 Z&quot;.

<a id="xml_indenting"></a>
### <a name="indenting"></a>Odsazení

Chcete-li zapsat odsazený kód XML, nastavte vlastnost **odsazení** na **hodnotu true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>Nastavení serializátorů XML pro jednotlivé typy

Můžete nastavit různé serializace XML pro různé typy CLR. Například můžete mít konkrétní datový objekt, který vyžaduje **XmlSerializer** pro zpětnou kompatibilitu. Pro tento objekt lze použít **XmlSerializer** a nadále používat **DataContractSerializer** pro jiné typy.

Chcete-li nastavit serializátor XML pro konkrétní typ, zavolejte **SetSerializer**.

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

Můžete určit **XmlSerializer** nebo libovolný objekt, který je odvozen z **XmlObjectSerializer**.

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>Odebrání formátovacího modulu JSON nebo XML

Můžete odebrat formátovací modul JSON nebo formátovací modul XML ze seznamu formátovacích modulů, pokud je nechcete používat. Hlavní důvody k tomu jsou tyto:

- Omezení odezvy webového rozhraní API na konkrétní typ média. Například se můžete rozhodnout podporovat pouze odpovědi JSON a odstranit formátovací modul XML.
- Chcete-li výchozí formátovací modul nahradit vlastním formátovacím modulem. Můžete například nahradit formátovací modul JSON vlastní implementací formátovacího modulu JSON.

Následující kód ukazuje, jak odebrat výchozí formátovací moduly. Tuto metodu zavolejte z vaší **aplikace\_metoda Start** definované v Global. asax.

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>Zpracování cyklických odkazů na objekty

Ve výchozím nastavení zapisují formátovací moduly JSON a XML všechny objekty jako hodnoty. Pokud dvě vlastnosti odkazují na stejný objekt, nebo pokud je stejný objekt v kolekci dvakrát zobrazen, formátovací modul tento objekt pozastaví dvakrát. Jedná se o konkrétní problém, pokud graf objektu obsahuje cykly, protože serializátor vyvolá výjimku, když detekuje smyčku v grafu.

Vezměte v úvahu následující objektové modely a kontroléry.

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

Vyvolání této akce způsobí, že formátovací modul vyvolal výjimku, která se přeloží na odpověď na stavový kód 500 (interní chyba serveru) na klienta.

Chcete-li zachovat odkazy na objekty ve formátu JSON, přidejte následující kód do metody **Application\_Start** v souboru Global. asax:

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

Nyní akce kontroleru vrátí JSON, která vypadá takto:

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

Všimněte si, že serializátor přidá vlastnost &quot;$id&quot; do obou objektů. Také zjistí, že vlastnost zaměstnanec. Department vytvoří smyčku, takže nahradí hodnotu odkazem na objekt: {&quot;$ref&quot;:&quot;1&quot;}.

> [!NOTE]
> Odkazy na objekty nejsou ve formátu JSON standardní. Před použitím této funkce zvažte, zda budou vaši klienti moci analyzovat výsledky. Může být vhodnější jednoduše odebrat cykly z grafu. Například odkaz od zaměstnance zpátky do oddělení není v tomto příkladu skutečně potřeba.

Chcete-li zachovat odkazy na objekty v XML, máte dvě možnosti. Jednodušší možností je přidat `[DataContract(IsReference=true)]` do třídy modelu. Parametr *IsReference* povoluje odkazy na objekty. Pamatujte, že **DataContract** zpřístupňuje serializaci, takže budete muset také přidat atributy **DataMember** do vlastností:

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

Modul formátování nyní vytvoří jazyk XML podobný následujícímu:

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

Pokud se chcete vyhnout atributům třídy modelu, existuje další možnost: Vytvořte novou instanci **DataContractSerializer** specifickou pro typ a nastavte *preserveObjectReferences* na **hodnotu true** v konstruktoru. Pak nastavte tuto instanci jako serializátor pro typ ve formátovacím modulu XML typu médium. Následující kód ukazuje, jak to provést:

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>Testování serializace objektu

Při návrhu webového rozhraní API je vhodné otestovat, jak budou datové objekty serializovány. Můžete to udělat bez vytvoření kontroleru nebo vyvolání akce kontroleru.

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]

---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'Posílání dat formuláře HTML ve webovém rozhraní API ASP.NET: form-urlencoded data – ASP.NET 4. x'
author: MikeWasson
description: Tento článek popisuje, jak publikovat data urlencoded formuláře do kontroleru webového rozhraní API s ASP.NET 4. x.
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557601"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a>Posílání dat formuláře HTML ve webovém rozhraní API ASP.NET: form-urlencoded data

o [Jan Wasson](https://github.com/MikeWasson)

## <a name="part-1-form-urlencoded-data"></a>1\. část: forma-urlencoded data

Tento článek ukazuje, jak odesílat data urlencoded formuláře do kontroleru webového rozhraní API.

- [Přehled formulářů HTML](#overview_of_html_forms)
- [Posílání složitých typů](#sending_complex_types)
- [Posílání dat formuláře prostřednictvím AJAX](#sending_form_data_via_ajax)
- [Posílání jednoduchých typů](#sending_simple_types)

> [!NOTE]
> [Stáhněte dokončený projekt](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a>Přehled formulářů HTML

Formuláře HTML používají k odesílání dat na server buď GET, nebo POST. Atribut **Method** prvku **Form** poskytuje metodu http:

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

Výchozí metoda je GET. Pokud formulář používá GET, data formuláře jsou v identifikátoru URI kódována jako řetězec dotazu. Pokud formulář používá POST, data formuláře se umístí do textu žádosti. V případě publikovaných dat určuje atribut **Enctype** formát textu žádosti:

| enctype | Popis |
| --- | --- |
| Application/x-www-form-urlencoded | Data formuláře jsou kódována jako páry název-hodnota, podobně jako řetězec dotazu identifikátoru URI. Toto je výchozí formát pro POST. |
| multipart/form-data | Data formuláře se kódují jako zpráva MIME s více částmi. Tento formát použijte při nahrávání souboru na server. |

Část 1 tohoto článku se zabývá formátem x-www-form-urlencoded. [Část 2](sending-html-form-data-part-2.md) popisuje MIME s více částmi.

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a>Posílání složitých typů

Obvykle odešlete složitý typ složený z hodnot pořízených z několika ovládacích prvků Form. Vezměte v úvahu následující model, který představuje aktualizaci stavu:

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

Tady je kontroler webového rozhraní API, který přijímá objekt `Update` prostřednictvím POST.

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> Tento kontroler používá [směrování na základě akcí](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), takže šablona trasy je &quot;API/{Controller}/{Action}/{id}&quot;. Klient odešle data do &quot;/API/Updates/Complex&quot;.

Nyní napíšeme formulář HTML pro uživatele, kteří odešlou aktualizaci stavu.

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

Všimněte si, že atribut **Action** formuláře je identifikátor URI naší akce kontroleru. Zde je formulář s některými hodnotami zadanými v:

![](sending-html-form-data-part-1/_static/image1.png)

Když uživatel klikne na Odeslat, prohlížeč odešle požadavek HTTP podobný následujícímu:

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

Všimněte si, že tělo žádosti obsahuje data formuláře formátovaná jako páry název-hodnota. Webové rozhraní API automaticky převede páry název/hodnota na instanci třídy `Update`.

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a>Posílání dat formuláře prostřednictvím AJAX

Když uživatel formulář odešle, prohlížeč přejde pryč z aktuální stránky a vykreslí text zprávy s odpovědí. To je v pořádku, když je odpověď stránka HTML. V případě webového rozhraní API je však tělo odpovědi obvykle prázdné nebo obsahuje strukturovaná data, jako je například JSON. V takovém případě je vhodnější odesílat data formuláře pomocí požadavku AJAX, aby stránka mohla zpracovat odpověď.

Následující kód ukazuje, jak publikovat data formuláře pomocí jQuery.

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

Funkce jQuery pro **odeslání** nahrazuje akci formuláře novou funkcí. Tím se přepíše výchozí chování tlačítka Odeslat. Funkce **serializace** serializace data formuláře na páry název-hodnota. Chcete-li odeslat data formuláře na server, zavolejte `$.post()`.

Po dokončení žádosti zobrazí obslužná rutina `.success()` nebo `.error()` příslušnou zprávu uživateli.

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a>Posílání jednoduchých typů

V předchozích částech jsme poslali komplexní typ, který webové rozhraní API deserializovat na instanci třídy modelu. Můžete také odesílat jednoduché typy, jako je například řetězec.

> [!NOTE]
> Před odesláním jednoduchého typu zvažte místo toho zabalení hodnoty do komplexního typu. To vám dává výhody ověřování modelu na straně serveru a usnadňuje tak rozšiřování modelu v případě potřeby.

Základní kroky pro odeslání jednoduchého typu jsou stejné, ale existují dva malé rozdíly. Nejprve je třeba v kontroleru vyplnit název parametru atributem **FromBody** .

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

Ve výchozím nastavení se webové rozhraní API pokusí získat jednoduché typy z identifikátoru URI požadavku. Atribut **FromBody** oznamuje webovému rozhraní API načtení hodnoty z textu žádosti.

> [!NOTE]
> Webové rozhraní API čte text odpovědi nejvíce jednou, takže z textu žádosti může pocházet pouze jeden parametr akce. Pokud potřebujete získat více hodnot z textu žádosti, definujte komplexní typ.

Druhý klient potřebuje odeslat hodnotu v následujícím formátu:

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

Konkrétně část názvu dvojice název/hodnota musí být pro jednoduchý typ prázdná. Ne všechny prohlížeče tuto podporu podporují pro formuláře HTML, ale tento formát vytvoříte ve skriptu následujícím způsobem:

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

Tady je příklad formuláře:

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

A zde je skript pro odeslání hodnoty formuláře. Jediným rozdílem z předchozího skriptu je argument předaný do funkce **post** .

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

Stejný přístup můžete použít k odeslání pole jednoduchých typů:

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a>Další prostředky

[Část 2: nahrání souboru a MIME s více částmi](sending-html-form-data-part-2.md)

---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'Posílání dat formuláře HTML ve webovém rozhraní API ASP.NET: nahrání souboru a MIME-ASP.NET 4. x'
author: MikeWasson
description: V tomto kurzu se dozvíte, jak nahrát soubory do webového rozhraní API. Popisuje také postup zpracování dat MIME v částech.
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557566"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a>Posílání dat formuláře HTML ve webovém rozhraní API ASP.NET: nahrání souboru a MIME s více částmi

o [Jan Wasson](https://github.com/MikeWasson)

## <a name="part-2-file-upload-and-multipart-mime"></a>Část 2: nahrání souboru a MIME s více částmi

V tomto kurzu se dozvíte, jak nahrát soubory do webového rozhraní API. Popisuje také postup zpracování dat MIME v částech.

> [!NOTE]
> [Stáhněte dokončený projekt](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).

Tady je příklad formuláře HTML pro nahrání souboru:

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

Tento formulář obsahuje ovládací prvek textové zadání a ovládací prvek vstupu do souboru. Pokud formulář obsahuje ovládací prvek vstupního souboru, atribut **Enctype** by měl vždy &quot;multipart/form-data&quot;, který určuje, že formulář bude odeslán jako zpráva MIME s více částmi.

Formát zprávy MIME s více částmi je nejjednodušší pochopit tím, že se podíváte na příklad požadavku:

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

Tato zpráva je rozdělena na dvě *části*, jednu pro každý ovládací prvek formuláře. Hranice součásti jsou označeny řádky, které začínají pomlčkami.

> [!NOTE]
> Hranice součásti zahrnuje náhodnou součást (&quot;41184676334&quot;), aby se zajistilo, že se řetězec hranice omylem neobjeví uvnitř části zprávy.

Každá část zprávy obsahuje jednu nebo více hlaviček následovaných obsahem části.

- Hlavička Content-Disposition obsahuje název ovládacího prvku. V případě souborů obsahuje také název souboru.
- Hlavička Content-Type popisuje data v části. Pokud je tato hlavička vynechána, výchozí hodnota je text/prostý.

V předchozím příkladu uživatel nahrál soubor s názvem GrandCanyon. jpg s typem obsahu image/jpeg; a hodnota textového vstupu byla &quot;letní dovolené&quot;.

## <a name="file-upload"></a>Nahrání souboru

Nyní se podívejme na kontroler webového rozhraní API, který čte soubory ze zprávy MIME s více částmi. Řadič bude soubory číst asynchronně. Webové rozhraní API podporuje asynchronní akce pomocí [programovacího modelu založeného na úlohách](https://msdn.microsoft.com/library/dd460693.aspx). Nejdřív je zde kód, pokud cílíte .NET Framework 4,5, které podporují klíčová slova **Async** a **await** .

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

Všimněte si, že akce kontroleru nepřijímá žádné parametry. To je proto, že zpracováváme tělo žádosti v rámci akce bez vyvolání formátovacího modulu typu média.

Metoda **IsMultipartContent** ověří, zda požadavek obsahuje zprávu MIME s více částmi. V takovém případě kontroler vrátí stavový kód HTTP 415 (nepodporovaný typ média).

Třída **MultipartFormDataStreamProvider** je pomocný objekt, který přiděluje datové proudy souborů pro nahrané soubory. Chcete-li si přečíst zprávu MIME s více částmi, zavolejte metodu **ReadAsMultipartAsync** . Tato metoda extrahuje všechny části zprávy a zapisuje je do datových proudů poskytovaných **MultipartFormDataStreamProvider**.

Po dokončení metody můžete získat informace o souborech z vlastnosti **dat** , což je kolekce objektů **MultipartFileData** .

- **MultipartFileData. FileName** je název místního souboru na serveru, kde byl soubor uložen.
- **MultipartFileData. Headers** obsahuje hlavičku části (*ne* hlavičku požadavku). Tuto možnost můžete použít pro přístup k obsahu\_k dispozici a k hlavičkám typu Content-Type.

Jak název naznačuje, **ReadAsMultipartAsync** je asynchronní metoda. K provedení práce po dokončení metody použijte [úlohu pokračování](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4,0) nebo klíčové slovo **await** (.NET 4,5).

Tady je verze .NET Framework 4,0 předchozího kódu:

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a>Čtení dat ovládacího prvku formulář

Formulář HTML, který jsem ukázal dříve, měl ovládací prvek textové zadání.

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

Hodnotu ovládacího prvku lze získat z vlastnosti **FormData** třídy **MultipartFormDataStreamProvider**.

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

**FormData** je **kolekce NameValueCollection** , který obsahuje páry název/hodnota pro ovládací prvky formuláře. Kolekce může obsahovat duplicitní klíče. Vezměte v úvahu tento formulář:

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

Text žádosti může vypadat takto:

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

V takovém případě by kolekce **FormData** obsahovala následující páry klíč/hodnota:

- cesta: zpáteční cesta
- možnosti: neukončeno
- možnosti: kalendářní data
- sedadlo: okno

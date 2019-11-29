---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: Volání služby OData z klienta .NET (C#) | Microsoft Docs
author: MikeWasson
description: V tomto kurzu se dozvíte, jak volat službu OData C# z klientské aplikace. Verze softwaru používané v tomto kurzu Visual Studio 2013 (funguje s Visual S...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600395"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a>Volání služby OData z klienta .NET (C#)

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> V tomto kurzu se dozvíte, jak volat službu OData C# z klientské aplikace.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (funguje se sadou Visual Studio 2012)
> - [Klientská knihovna pro WCF Data Services](https://msdn.microsoft.com/library/cc668772.aspx)
> - Webové rozhraní API 2 (Ukázková Služba OData je sestavená pomocí webového rozhraní API 2, ale klientská aplikace nezávisí na webovém rozhraní API.)

V tomto kurzu Vás provedeme vytvořením klientské aplikace, která volá službu OData. Služba OData zpřístupňuje následující entity:

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

Následující články popisují implementaci služby OData ve webovém rozhraní API. (K pochopení tohoto kurzu ale nemusíte číst.)

- [Vytvoření koncového bodu OData ve webovém rozhraní API 2](creating-an-odata-endpoint.md)
- [Vztahy entit OData ve webovém rozhraní API 2](working-with-entity-relations.md)
- [Akce OData ve webovém rozhraní API 2](odata-actions.md)

## <a name="generate-the-service-proxy"></a>Vygenerovat proxy služby

Prvním krokem je vygenerování proxy služby. Proxy služby je třída rozhraní .NET, která definuje metody pro přístup ke službě OData. Proxy překládá volání metod na požadavky HTTP.

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

Začněte otevřením projektu služby OData v aplikaci Visual Studio. Stisknutím kombinace kláves CTRL + F5 spusťte službu místně v IIS Express. Poznamenejte si místní adresu, včetně čísla portu, které Visual Studio přiřadí. Tuto adresu budete potřebovat při vytváření proxy serveru.

Potom otevřete jinou instanci aplikace Visual Studio a vytvořte projekt konzolové aplikace. Konzolová aplikace bude naše klientská aplikace OData. (Projekt můžete také přidat ke stejnému řešení jako služba.)

> [!NOTE]
> Zbývající kroky odkazují na projekt konzoly.

V Průzkumník řešení klikněte pravým tlačítkem na **odkazy** a vyberte **Přidat odkaz na službu**.

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

V dialogovém okně **Přidat odkaz na službu** zadejte adresu služby OData:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

kde *port* je číslo portu.

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

Do možnosti **obor názvů**zadejte "ProductService". Tato možnost definuje obor názvů třídy proxy serveru.

Klikněte na **Přejít**. Visual Studio přečte dokument metadat OData, ve kterém zjistí entity ve službě.

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

Kliknutím na tlačítko **OK** přidejte třídu proxy do projektu.

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a>Vytvoření instance proxy třídy služby

V rámci metody `Main` vytvořte novou instanci třídy proxy následujícím způsobem:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

Znovu použijte skutečné číslo portu, ve kterém je vaše služba spuštěná. Při nasazení služby použijete identifikátor URI živé služby. Nemusíte aktualizovat proxy server.

Následující kód přidá obslužnou rutinu události, která vytiskne identifikátor URI žádosti do okna konzoly. Tento krok není povinný, ale je zajímavé zobrazit identifikátory URI pro každý dotaz.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a>Dotazování služby

Následující kód získá seznam produktů ze služby OData.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

Všimněte si, že nemusíte psát žádný kód pro odeslání požadavku HTTP nebo analýzu odpovědi. Třída proxy to provede automaticky při vytváření výčtu kolekce `Container.Products` ve smyčce **foreach** .

Když aplikaci spustíte, výstup by měl vypadat takto:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

Chcete-li získat entitu podle ID, použijte klauzuli `where`.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

Pro zbytek tohoto tématu nezobrazujeme celou `Main` funkci, jenom kód potřebný k volání služby.

## <a name="apply-query-options"></a>Použít možnosti dotazu

OData definuje [Možnosti dotazu](../supporting-odata-query-options.md) , které se dají použít k filtrování, řazení, stránkování dat a tak dále. V proxy službě můžete tyto možnosti použít pomocí různých výrazů LINQ.

V této části se zobrazí stručné příklady. Další podrobnosti najdete v tématu věnovaném [hlediskům LINQ (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) na webu MSDN.

### <a name="filtering-filter"></a>Filtrování ($filter)

Chcete-li filtrovat, použijte klauzuli `where`. Následující příklad filtruje podle kategorie produktu.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

Tento kód odpovídá následujícímu dotazu OData.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

Všimněte si, že proxy převede klauzuli `where` na výraz `$filter` OData.

### <a name="sorting-orderby"></a>Řazení ($orderby)

K řazení použijte klauzuli `orderby`. Následující příklad seřadí podle ceny od nejvyšších po nejnižší.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

Zde je odpovídající požadavek OData.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a>Stránkování na straně klienta ($skip a $top)

U rozsáhlých sad entit může klient chtít omezit počet výsledků. Klient může například zobrazit 10 položek najednou. Označuje se jako *stránkování na straně klienta*. (K dispozici je také [stránkování na straně serveru](../supporting-odata-query-options.md#server-paging), kde server omezuje počet výsledků.) Chcete-li provést stránkování na straně klienta, použijte metody LINQ **Skip** a **probrat** . Následující příklad přeskočí prvních 40 výsledků a provede následující 10.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

Toto je odpovídající požadavek OData:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a>Select ($select) a expand ($expand)

Chcete-li zahrnout související entity, použijte metodu `DataServiceQuery<t>.Expand`. Pokud například chcete zahrnout `Supplier` pro každý `Product`:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

Toto je odpovídající požadavek OData:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

Chcete-li změnit tvar odpovědi, použijte klauzuli LINQ **Select** . Následující příklad získá jenom název každého produktu bez dalších vlastností.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

Toto je odpovídající požadavek OData:

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

Klauzule SELECT může zahrnovat související entity. V takovém případě Nevolejte příkaz **expand**; proxy server automaticky obsahuje rozšíření v tomto případě. Následující příklad získá název a dodavatel každého produktu.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

Zde je odpovídající požadavek OData. Všimněte si, že obsahuje možnost **$expand** .

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

Další informace o $select a $expand najdete v tématu [použití $Select, $expand a $Value ve webovém rozhraní API 2](../using-select-expand-and-value.md).

## <a name="add-a-new-entity"></a>Přidat novou entitu

Chcete-li přidat novou entitu do sady entit, zavolejte `AddToEntitySet`, kde *EntitySet* je název sady entit. `AddToProducts` například přidá novou `Product` do sady entit `Products`. Když vygenerujete proxy server, WCF Data Services automaticky vytvoří tyto metody silného typu **AddTo** .

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

Chcete-li přidat propojení mezi dvěma entitami, použijte metody **addlink** a **SetLink** . Následující kód přidá nového dodavatele a nový produkt a vytvoří propojení mezi nimi.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

Pokud je navigační vlastnost kolekce, použijte **addlink** . V tomto příkladu přidáme produkt do kolekce `Products` na dodavatele.

Pokud je navigační vlastnost jediná entita, použijte **SetLink** . V tomto příkladu nastavujeme vlastnost `Supplier` v produktu.

## <a name="update--patch"></a>Aktualizovat/opravit

Chcete-li aktualizovat entitu, zavolejte metodu **UpdateObject** .

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

Aktualizace je provedena při volání **metody SaveChanges**. Ve výchozím nastavení posílá WCF požadavek na sloučení HTTP. Možnost **PatchOnUpdate** instruuje WCF, aby místo toho odeslal opravu http.

> [!NOTE]
> Proč je oprava oproti sloučení? Původní specifikace protokolu HTTP 1,1 ([RCF 2616](http://tools.ietf.org/html/rfc2616)) nedefinovala žádnou metodu HTTP se sémantikou "částečná aktualizace". Pro podporu částečných aktualizací specifikace OData definovala metodu sloučení. V 2010 se v [RFC 5789](http://tools.ietf.org/html/rfc5789) definovala metoda opravy pro částečné aktualizace. V tomto [příspěvku blogu](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) na blogu WCF Data Services si můžete přečíst některé historie. V současné době se při sloučení upřednostňuje oprava. Kontroler OData vytvořený pomocí generování uživatelského rozhraní webového rozhraní API podporuje obě metody.

Pokud chcete nahradit celou entitu (uvést sémantiku), zadejte možnost **ReplaceOnUpdate** . To způsobí, že WCF odešle požadavek HTTP PUT.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a>Odstranění entity

Pokud chcete entitu odstranit, zavolejte na **OdstranitObjekt**.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a>Vyvolat akci OData

V OData představují [Akce](odata-actions.md) způsob, jak přidat chování na straně serveru, které není snadno definované jako operace CRUD u entit.

I když dokument metadat OData popisuje akce, Třída proxy nevytváří pro ně žádné metody silného typu. Můžete přesto vyvolat akci OData pomocí obecné metody **Execute** . Budete ale muset znát datové typy parametrů a vrácenou hodnotu.

Například akce `RateProduct` přijímá parametr s názvem "hodnocení" typu `Int32` a vrátí `double`. Následující kód ukazuje, jak tuto akci vyvolat.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

Další informace najdete v tématu[volání operací a akcí služby](https://msdn.microsoft.com/library/hh230677.aspx).

Jednou z možností je zvětšit třídu **kontejneru** tak, aby poskytovala metodu silného typu, která vyvolá tuto akci:

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]

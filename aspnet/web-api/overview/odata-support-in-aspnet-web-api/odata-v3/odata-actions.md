---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: Podpora akcí OData ve webovém rozhraní API 2 ASP.NET | Microsoft Docs
author: MikeWasson
description: 'V OData představují akce způsob, jak přidat chování na straně serveru, které není snadno definované jako operace CRUD u entit. Některá použití pro akce zahrnují: implementovat...'
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556355"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a>Podpora akcí OData ve webovém rozhraní API 2 ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> V OData představují *Akce* způsob, jak přidat chování na straně serveru, které není snadno definované jako operace CRUD u entit. Mezi tato použití pro akce patří:
> 
> - Implementace složitých transakcí.
> - Manipulace s několika entitami najednou.
> - Povoluje se aktualizace pouze některých vlastností entity.
> - Odesílají se informace na server, který není definovaný v entitě.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové rozhraní API 2
> - OData verze 3
> - Entity Framework 6

## <a name="example-rating-a-product"></a>Příklad: hodnocení produktu

V tomto příkladu chceme dovolit uživatelům hodnotit množství produktů a pak vystavit Průměrné hodnocení pro každý produkt. V databázi budeme uchovávat seznam hodnocení, označených pro produkty.

Tady je model, který můžeme použít k reprezentaci hodnocení v Entity Framework:

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

Ale nechcete, aby klienti mohli publikovat objekt `ProductRating` do kolekce hodnocení. V intuitivním případě je hodnocení přidruženo k kolekci Products a klient by měl pouze vystavit hodnotu hodnocení.

Proto namísto použití běžných operací CRUD definujeme akci, kterou může klient vyvolat na produkt. V terminologii OData je akce *svázána* s entitami produktů.

>Akce mají v serveru vedlejší účinky. Z tohoto důvodu jsou vyvolány pomocí požadavků HTTP POST. Akce mohou mít parametry a návratové typy, které jsou popsány v metadatech služby. Klient odešle parametry v textu požadavku a server odešle vrácenou hodnotu v těle odpovědi. Aby mohl klient vyvolat akci "hodnotit produkt", odešle příspěvek na identifikátor URI podobný následujícímu:

[!code-console[Main](odata-actions/samples/sample2.cmd)]

Data v žádosti POST jsou jednoduše hodnocením produktu:

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a>Deklarovat akci v model EDM (Entity Data Model)

V konfiguraci webového rozhraní API přidejte akci do modelu Entity Data Model (EDM):

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

Tento kód definuje "RateProduct" jako akci, kterou lze provést u entit produktu. Deklaruje také, že akce přijímá parametr **int** s názvem "hodnocení" a vrátí hodnotu typu **int** .

## <a name="add-the-action-to-the-controller"></a>Přidat akci do kontroleru

Akce "RateProduct" je svázána s entitami produktů. Chcete-li implementovat akci, přidejte do kontroleru produktů metodu s názvem `RateProduct`:

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

Všimněte si, že název metody se shoduje s názvem akce v EDM. Metoda má dva parametry:

- *Key*(klíč): klíč pro produkt, který se má ohodnotit.
- *parametry*: slovník hodnot parametrů akce.

Pokud používáte výchozí konvence směrování, parametr klíče musí být pojmenovaný "klíč". Je také důležité zahrnout atribut **[FromOdataUri]** , jak je znázorněno v příkladu. Tento atribut oznamuje webovému rozhraní API použití pravidel syntaxe OData při analýze klíče z identifikátoru URI požadavku.

Parametry akce získáte pomocí slovníku *parametrů* :

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

Pokud klient odešle parametry akce ve správném formátu, hodnota **ModelState. IsValid** má hodnotu true. V takovém případě můžete použít slovník **ODataActionParameters** k získání hodnot parametrů. V tomto příkladu akce `RateProduct` přijímá jeden parametr s názvem "hodnocení".

## <a name="action-metadata"></a>Metadata akce

Pokud chcete zobrazit metadata služby, odešlete požadavek GET na/OData/$metadata. Tady je část metadat, která deklaruje `RateProduct` akci:

[!code-xml[Main](odata-actions/samples/sample7.xml)]

Element **FunctionImport** deklaruje akci. Většina polí je zřejmá, ale dvě se zaznamená:

- S možností **vazby** znamená, že akci lze vyvolat v cílové entitě alespoň v některých časových okamžikech.
- **IsAlwaysBindable** znamená, že akce může být vždy vyvolána v cílové entitě.

Rozdílem je, že některé akce jsou vždy k dispozici klientům, ale jiné akce mohou záviset na stavu entity. Předpokládejme například, že definujete akci "koupit". Můžete koupit jenom položku, která je na skladě. Pokud je položka neskladovaná, klient nemůže tuto akci vyvolat.

Při definování EDM metoda **Akce** vytvoří akci Always-BIND:

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

Dále v tomto tématu se dozvíte o akcích, které nejsou vždy vázané na vazby (označované také jako *přechodné* akce).

## <a name="invoking-the-action"></a>Vyvolání akce

Teď se podívejme, jak by klient tuto akci vyvolal. Předpokládejme, že klient chce dát hodnocení 2 k produktu s ID = 4. Tady je příklad zprávy s požadavkem s použitím formátu JSON pro tělo žádosti:

[!code-console[Main](odata-actions/samples/sample9.cmd)]

Tady je zpráva odpovědi:

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a>Navázání akce na sadu entit

V předchozím příkladu je akce svázána s jedinou entitou: klient vyhodnotí jeden produkt. Akci můžete také navazovat na kolekci entit. Pouze proveďte následující změny:

V datovém modelu EDM přidejte akci do vlastnosti **kolekce** entity.

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

V metodě Controller vynechejte parametr *klíče* .

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

Klient nyní vyvolá akci pro sadu entit Products:

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a>Akce s parametry kolekce

Akce mohou mít parametry, které přijímají kolekci hodnot. V datovém modelu EDM použijte **&gt;CollectionParameter&lt;t** k deklaraci parametru.

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

Tato deklarace deklaruje parametr s názvem "hodnocení", který přebírá kolekci hodnot **int** . V metodě Controller stále získáte hodnotu parametru z objektu **ODataActionParameters** , ale nyní je hodnotou hodnota typu **ICollection&lt;int&gt;** :

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a>Přechodné akce

V příkladu "RateProduct" můžou uživatelé vždycky Ohodnotit produkt, takže tato akce je vždycky dostupná. Některé akce ale závisí na stavu entity. Například u služby pronájmu videa není akce "rezervace" vždy k dispozici. (Záleží na tom, jestli je kopie tohoto videa dostupná.) Tento typ akce se nazývá *přechodná* akce.

V metadatech služby je přechodná akce **IsAlwaysBindable** rovna hodnotě false. To je vlastně výchozí hodnota, takže metadata budou vypadat takto:

[!code-xml[Main](odata-actions/samples/sample16.xml)]

Z tohoto důvodu: Pokud je akce přechodná, server musí klientovi sdělit, že je akce k dispozici. Zahrnuje odkaz na akci v entitě. Tady je příklad pro entitu video:

[!code-console[Main](odata-actions/samples/sample17.cmd)]

Vlastnost "#CheckOut" obsahuje odkaz na akci rezervace. Pokud akce není k dispozici, server odkaz vynechá.

Chcete-li deklarovat přechodnou akci v modelu EDM, zavolejte metodu **TransientAction** :

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

Také je nutné zadat funkci, která vrátí odkaz akce pro danou entitu. Tuto funkci nastavíte voláním **HasActionLink**. Funkci můžete napsat jako výraz lambda:

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

Pokud je akce k dispozici, výraz lambda vrátí odkaz na akci. Serializátor OData obsahuje tento odkaz při serializaci entity. Pokud akce není k dispozici, funkce vrátí `null`.

## <a name="additional-resources"></a>Další prostředky

[Ukázka akcí OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)

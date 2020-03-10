---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: Směrování a výběr akcí ve webovém rozhraní API ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554885"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a>Směrování a výběr akcí ve webovém rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Tento článek popisuje, jak webové rozhraní API ASP.NET směruje požadavek HTTP na určitou akci na řadiči.

> [!NOTE]
> Podrobný přehled směrování najdete v tématu [směrování ve webovém rozhraní API ASP.NET](routing-in-aspnet-web-api.md).

V tomto článku se podíváme na podrobnosti o procesu směrování. Pokud vytvoříte projekt webového rozhraní API a zjistíte, že některé požadavky nejsou směrovány očekávaným způsobem, snad tohoto článku vám pomůže.

Směrování má tři hlavní fáze:

1. Identifikátor URI se shoduje s šablonou trasy.
2. Výběr kontroleru.
3. Výběr akce

Některé části procesu můžete nahradit vlastními chováními. V tomto článku jsme popsali výchozí chování. Na konci se označují místa, kde můžete přizpůsobit chování.

## <a name="route-templates"></a>Šablony směrování

Šablona trasy vypadá podobně jako cesta URI, ale může mít zástupné hodnoty označené složenými závorkami:

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

Při vytváření trasy můžete zadat výchozí hodnoty pro některé nebo všechny zástupné symboly:

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

Můžete také poskytnout omezení, která omezují, jak může segment URI odpovídat zástupnému symbolu:

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

Rozhraní se pokusí vyhledat segmenty v cestě identifikátoru URI k šabloně. Literály v šabloně se musí přesně shodovat. Zástupný text odpovídá jakékoli hodnotě, pokud nezadáte omezení. Rozhraní se neshoduje s ostatními částmi identifikátoru URI, jako je název hostitele nebo parametry dotazu. Rozhraní vybere první trasu v tabulce směrování, která odpovídá identifikátoru URI.

Existují dva speciální zástupné symboly: {Controller} a {Action}.

- {Controller} poskytuje název kontroleru.
- "{Action}" poskytuje název akce. V rámci webového rozhraní API je obvyklá konvence vynechat {Action}.

### <a name="defaults"></a>Ve výchozím nastavení

Pokud zadáte výchozí hodnoty, bude trasa odpovídat identifikátoru URI, u kterého tyto segmenty chybí. Příklad:

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

Identifikátory URI `http://localhost/api/products/all` a `http://localhost/api/products` odpovídají předchozí trase. V druhém identifikátoru URI má `{category}` k chybějícímu segmentu přiřazenou výchozí hodnotu `all`.

### <a name="route-dictionary"></a>Slovník směrování

Pokud rozhraní nalezne shodu pro identifikátor URI, vytvoří slovník, který obsahuje hodnotu pro každý zástupný text. Klíče jsou zástupné názvy, včetně složených závorek. Hodnoty jsou přijímány z cesty identifikátoru URI nebo z výchozího nastavení. Slovník je uložen v objektu **IHttpRouteData** .

Během této fáze pro porovnání tras se speciální zástupné symboly {Controller} a {Action} považují za stejné jako jiné zástupné symboly. Jsou jednoduše uloženy ve slovníku s ostatními hodnotami.

Výchozí hodnota může mít speciální hodnotu **RouteParameter. volitelné**. Pokud se této hodnotě přiřadí zástupný text, hodnota se nepřidá do slovníku směrování. Příklad:

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

Pro cestu identifikátoru URI "API/Products" bude mít slovník tras:

- kontroler: "Products"
- Kategorie: vše

Pro "API/Products/Toys/123" ale bude mít tento slovník tras:

- kontroler: "Products"
- Kategorie: "hračky"
- ID: "123"

Výchozí hodnoty mohou také obsahovat hodnotu, která se nezobrazí kdekoli v šabloně trasy. Pokud trasa odpovídá, je tato hodnota uložena ve slovníku. Příklad:

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

Pokud je cesta URI "API/root/8", bude mít slovník dvě hodnoty:

- kontroler: "Customers"
- ID: "8"

## <a name="selecting-a-controller"></a>Výběr kontroleru

Výběr kontroleru se zpracovává metodou **IHttpControllerSelector. SelectController** . Tato metoda přebírá instanci **zprávy HttpRequestMessage** a vrací **HttpControllerDescriptor**. Výchozí implementace je poskytována třídou **DefaultHttpControllerSelector** . Tato třída používá přímočarý algoritmus:

1. Podívejte se do slovníku tras pro klíč "Controller".
2. Pokud chcete získat název typu kontroléru, přečtěte si hodnotu tohoto klíče a přidejte do něj řetězec "Controller".
3. Vyhledejte kontroler webového rozhraní API s tímto názvem typu.

Pokud například adresář tras obsahuje dvojici klíč-hodnota "Controller" = "Products", pak je typ kontroleru "ProductsController". Pokud neexistuje odpovídající typ ani více shod, rozhraní vrátí chybu klientovi.

V kroku 3 **DefaultHttpControllerSelector** používá rozhraní **IHttpControllerTypeResolver** k získání seznamu typů řadičů webového rozhraní API. Výchozí implementace **IHttpControllerTypeResolver** vrátí všechny veřejné třídy, které (a) implementují **IHttpController**, (b) nejsou abstraktní a (c) mají název, který končí na "Controller".

## <a name="action-selection"></a>Výběr akce

Po výběru kontroleru vybere architektura akci voláním metody **IHttpActionSelector. SelectAction** . Tato metoda přijímá **HttpControllerContext** a vrací **HttpActionDescriptor**.

Výchozí implementace je poskytována třídou **ApiControllerActionSelector** . Pokud chcete vybrat akci, podívejte se na následující:

- Metoda HTTP požadavku.
- Zástupný symbol {Action} v šabloně směrování, pokud je k dispozici.
- Parametry akcí na řadiči.

Než začnete s algoritmem výběru, musíme pochopit některé věci o akcích kontroleru.

**Které metody kontroleru se považují za "akce"?** Při výběru akce rozhraní vyhledá pouze veřejné metody instance v řadiči. Kromě toho vylučuje metody ["speciálního názvu"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) (konstruktory, události, přetížení operátoru a tak dále) a metody zděděné z třídy **ApiController** .

**Metody HTTP.** Rozhraní vybere pouze akce, které odpovídají metodě HTTP žádosti, určené následujícím způsobem:

1. Metodu HTTP můžete zadat s atributem: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HTTPPOST**nebo **HttpPut**.
2. V opačném případě, pokud název metody kontroleru začíná na "Get", "post", "Put", "Delete", "Head", "Options" nebo "patch", pak podle konvence akce podporuje tuto metodu HTTP.
3. Pokud žádný z výše uvedeného není, metoda podporuje POST.

**Vazby parametrů** Vazba parametru je způsob, jakým webové rozhraní API vytvoří hodnotu pro parametr. Toto je výchozí pravidlo pro vazbu parametru:

- Z identifikátoru URI jsou přijímány jednoduché typy.
- Komplexní typy jsou odebírány z textu žádosti.

Jednoduché typy zahrnují všechny [.NET Framework primitivních typů](https://msdn.microsoft.com/library/system.type.isprimitive)plus **DateTime**, **Decimal**, **GUID**, **String**a **TimeSpan**. Pro každou akci může tělo žádosti přečíst maximálně jeden parametr.

> [!NOTE]
> Je možné přepsat výchozí pravidla vazby. Viz [vazba parametrů WebApi v digestoři](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).

S tímto pozadím je tady algoritmus výběru akce.

1. Vytvoří seznam všech akcí na řadiči, které odpovídají metodě požadavku HTTP.
2. Pokud má slovník tras položku "Action" (akce), odeberte akce, jejichž název neodpovídá této hodnotě.
3. Zkuste porovnat parametry akce s identifikátorem URI následujícím způsobem: 

    1. Pro každou akci Získejte seznam parametrů, které jsou jednoduchého typu, kde vazba získá parametr z identifikátoru URI. Vylučte volitelné parametry.
    2. V tomto seznamu zkuste najít shodu pro každý název parametru, a to buď ve slovníku směrování, nebo v řetězci dotazu URI. Shoda rozlišuje velká a malá písmena a nezávisí na pořadí parametrů.
    3. Vyberte akci, u které má každý parametr v seznamu shodu s identifikátorem URI.
    4. Pokud tato kritéria splňují více než jedna akce, vyberte ji s nejvíce shodami parametrů.
4. Ignoruje akce s atributem **[neaction]** .

Krok #3 je pravděpodobně nejvíce matoucí. Základní nápad je, že parametr může získat svou hodnotu buď z identifikátoru URI, z textu žádosti, nebo z vlastní vazby. Pro parametry, které pocházejí z identifikátoru URI, chceme zajistit, aby identifikátor URI ve skutečnosti obsahoval hodnotu pro tento parametr, buď v cestě (prostřednictvím slovníku směrování), nebo v řetězci dotazu.

Zvažte například následující akci:

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

Parametr *ID* se váže k identifikátoru URI. Proto se tato akce může shodovat jenom s identifikátorem URI, který obsahuje hodnotu pro "ID", a to buď ve slovníku směrování, nebo v řetězci dotazu.

Volitelné parametry jsou výjimkou, protože jsou nepovinné. U volitelného parametru je to v pořádku, pokud vazba nemůže získat hodnotu z identifikátoru URI.

Komplexní typy jsou výjimkou z jiného důvodu. Komplexní typ se dá svázat jenom s identifikátorem URI prostřednictvím vlastní vazby. V takovém případě ale rozhraní nemůže bez ohledu na to, jestli parametr vytvoří vazby na konkrétní identifikátor URI. Aby bylo možné zjistit, bude nutné vyvolat vazbu. Cílem algoritmu výběru je vybrat akci ze statického popisu před vyvoláním jakýchkoli vazeb. Proto jsou komplexní typy vyloučeny z odpovídajícího algoritmu.

Po výběru akce jsou vyvolány všechny vazby parametrů.

Souhrn:

- Akce musí odpovídat metodě HTTP žádosti.
- Název akce se musí shodovat s položkou "Action" ve slovníku směrování, pokud je k dispozici.
- U každého parametru akce, pokud je parametr z identifikátoru URI, musí být název parametru nalezen buď ve slovníku směrování, nebo v řetězci dotazu identifikátoru URI. (Volitelné parametry a parametry se složitými typy jsou vyloučeny.)
- Snažte se porovnat s největším počtem parametrů. Nejlepší shoda může být metoda bez parametrů.

## <a name="extended-example"></a>Rozšířený příklad

Tras

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

Kontroler:

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

Požadavek HTTP:

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a>Shoda trasy

Identifikátor URI odpovídá trase s názvem "DefaultApi". Slovník tras obsahuje následující položky:

- kontroler: "Products"
- ID: "1"

Slovník tras neobsahuje parametry řetězce dotazu, "Version" a "Details", ale ty se budou i nadále brát v potaz během výběru akce.

### <a name="controller-selection"></a>Výběr kontroleru

Z položky "Controller" v adresáři směrování je typ kontroleru `ProductsController`.

### <a name="action-selection"></a>Výběr akce

Požadavek HTTP je požadavek GET. Akce kontroleru, které podporují GET, jsou `GetAll`, `GetById`a `FindProductsByName`. Slovník tras neobsahuje položku "Action", takže nemusíme odpovídat názvu akce.

V dalším kroku se podíváme na názvy parametrů pro akce, a to jenom v akci GET.

| Akce | Parametry, které se mají spárovat |
| --- | --- |
| `GetAll` | Žádná |
| `GetById` | účet |
| `FindProductsByName` | název |

Všimněte si, že parametr *verze* `GetById` není považován za, protože se jedná o volitelný parametr.

Metoda `GetAll` odpovídá triviálnímu. Metoda `GetById` také odpovídá, protože slovník směrování obsahuje "ID". Metoda `FindProductsByName` se neshoduje.

Služba `GetById` metoda WINS, protože se shoduje s jedním parametrem, bez parametrů pro `GetAll`. Metoda je vyvolána s následujícími hodnotami parametrů:

- *ID* = 1
- *verze* = 1,5

Všimněte si, že i když se *verze* v algoritmu výběru nepoužila, hodnota parametru přichází z řetězce dotazu identifikátoru URI.

## <a name="extension-points"></a>Rozšiřovací body

Webové rozhraní API poskytuje body rozšíření pro některé části procesu směrování.

| Rozhraní | Popis |
| --- | --- |
| **IHttpControllerSelector** | Vybere kontroler. |
| **IHttpControllerTypeResolver** | Získá seznam typů kontroléru. **DefaultHttpControllerSelector** zvolí typ kontroleru z tohoto seznamu. |
| **IAssembliesResolver** | Získá seznam sestavení projektu. Rozhraní **IHttpControllerTypeResolver** používá tento seznam k nalezení typů kontroleru. |
| **IHttpControllerActivator** | Vytvoří nové instance kontroleru. |
| **IHttpActionSelector** | Vybere akci. |
| **IHttpActionInvoker** | Vyvolá akci. |

K poskytnutí vlastní implementace pro některá z těchto rozhraní použijte kolekci **Services** na objektu **HttpConfiguration** :

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]

---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: Ověřování a autorizace ve webovém rozhraní API ASP.NET | Microsoft Docs
author: MikeWasson
description: Poskytuje obecný přehled o ověřování a autorizaci ve webovém rozhraní API ASP.NET.
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598642"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>Ověřování a autorizace v rozhraní ASP.NET Web API

o [Jan Wasson](https://github.com/MikeWasson)

Vytvořili jste webové rozhraní API, ale teď chcete řídit přístup k němu. V této sérii článků se podíváme na některé možnosti zabezpečení webového rozhraní API před neoprávněnými uživateli. Tato série se zabývá ověřováním i autorizací.

- *Ověřování* má na vědomí identitu uživatele. Například Alice se přihlásí pomocí svého uživatelského jména a hesla a server používá heslo k ověření Alice.
- *Autorizace* se rozhoduje, jestli uživatel může provést akci. Například Alice má oprávnění k získání prostředku, ale ne k vytvoření prostředku.

První článek v řadě poskytuje obecný přehled o ověřování a autorizaci ve webovém rozhraní API ASP.NET. Další témata popisují běžné scénáře ověřování pro webové rozhraní API.

> [!NOTE]
> Díky lidem, kteří si tuto řadu přezkoumali a získali si užitečnou zpětnou vazbu: Rick Anderson, dávka Broderick, Barryho Dorrans, Dykstra, Hongmei GE, David Matson, Daniel Skořepa, Tim Teebken.

## <a name="authentication"></a>Ověřování

Webové rozhraní API předpokládá, že k ověřování dojde v hostiteli. V případě webového hostování je hostitelem služba IIS, která pro ověřování používá moduly HTTP. Svůj projekt můžete nakonfigurovat tak, aby používal kterýkoli z modulů ověřování integrovaných ve službě IIS nebo ASP.NET, nebo napsat vlastní modul HTTP k provedení vlastního ověřování.

Když hostitel ověří uživatele, vytvoří objekt *zabezpečení*, což je objekt [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) , který představuje kontext zabezpečení, pod kterým je spuštěn kód. Hostitel připojí objekt zabezpečení k aktuálnímu vláknu nastavením **Thread. CurrentPrincipal**. Objekt zabezpečení obsahuje přidružený objekt **identity** , který obsahuje informace o uživateli. Pokud je uživatel ověřený, vlastnost **identity. Authenticated** vrátí **hodnotu true**. U anonymních požadavků vrátí **ověřování** **NEPRAVDA**. Další informace o objektech zabezpečení naleznete v tématu [zabezpečení na základě rolí](https://msdn.microsoft.com/library/shz8h065.aspx).

### <a name="http-message-handlers-for-authentication"></a>Obslužné rutiny zpráv HTTP pro ověřování

Namísto použití hostitele k ověřování můžete do [obslužné rutiny zpráv HTTP](../advanced/http-message-handlers.md)umístit logiku ověřování. V takovém případě obslužná rutina zprávy prověřuje požadavek HTTP a nastaví objekt zabezpečení.

Kdy byste měli použít obslužné rutiny zpráv pro ověřování? Zde jsou některé kompromisy:

- Modul HTTP vidí všechny požadavky, které procházejí kanálem ASP.NET. Obslužná rutina zprávy vidí pouze požadavky směrované do webového rozhraní API.
- Můžete nastavit obslužné rutiny zpráv pro jednotlivé trasy, které vám umožní použít schéma ověřování pro konkrétní trasu.
- Moduly HTTP jsou specifické pro službu IIS. Obslužné rutiny zpráv jsou hostitel – nezávislá, takže je lze použít jak pro hostování webu, tak pro samoobslužné hostování.
- Moduly HTTP se účastní protokolování, auditování a dalších služeb IIS.
- Moduly HTTP se spouští dříve v kanálu. Pokud zpracováváte ověřování v obslužné rutině zprávy, objekt zabezpečení se nezíská, dokud se obslužná rutina nespustí. Objekt zabezpečení se navíc vrátí zpět k předchozímu objektu zabezpečení, když odpověď opustí popisovač zprávy.

Obecně platí, že pokud nepotřebujete podporovat samoobslužné hostování, je modul HTTP lepší volbou. Pokud potřebujete podporu samoobslužného hostování, zvažte obslužnou rutinu zprávy.

### <a name="setting-the-principal"></a>Nastavení objektu zabezpečení

Pokud vaše aplikace provádí vlastní logiku ověřování, je nutné nastavit objekt zabezpečení na dvou místech:

- **Thread. CurrentPrincipal**. Tato vlastnost je standardní způsob, jak nastavit objekt zabezpečení vlákna v rozhraní .NET.
- **HttpContext. Current. User**. Tato vlastnost je specifická pro ASP.NET.

Následující kód ukazuje, jak nastavit objekt zabezpečení:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

V případě webového hostování je nutné nastavit objekt zabezpečení na obou místech. v opačném případě může dojít k nekonzistenci kontextu zabezpečení. Pro samoobslužné hostování však **vlastnost HttpContext. Current** má hodnotu null. Chcete-li zajistit, aby byl váš kód hostitelem – nezávislá, zkontrolujte před přiřazením do **HttpContext. Current**hodnotu null, jak je znázorněno v příkladu.

## <a name="authorization"></a>Autorizace

Autorizace se stane později v kanálu, a to blíž k řadiči. Díky tomu můžete při udělování přístupu k prostředkům provádět přesnější volby.

- *Filtry autorizace* se spouštějí před akcí kontroleru. Pokud požadavek není autorizován, vrátí filtr chybovou odpověď a akce není vyvolána.
- V rámci akce kontroleru můžete získat aktuální objekt zabezpečení z vlastnosti **ApiController. User** . Můžete například filtrovat seznam prostředků na základě uživatelského jména a vracet pouze ty prostředky, které patří tomuto uživateli.

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>Použití atributu [autorizovat]

Webové rozhraní API poskytuje vestavěný autorizační filtr [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx). Tento filtr ověří, zda je uživatel ověřený. Pokud ne, vrátí stavový kód HTTP 401 (Neautorizováno) bez vyvolání akce.

Filtr můžete použít globálně, na úrovni řadiče nebo na úrovni jednotlivých akcí.

**Globálně**: Pokud chcete omezit přístup pro každý kontroler webového rozhraní API, přidejte do seznamu globálních filtrů filtr **AuthorizeAttribute** :

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**Kontroler**: Chcete-li omezit přístup pro určitý kontroler, přidejte filtr do kontroleru jako atribut:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**Akce**: Chcete-li omezit přístup pro určité akce, přidejte atribut do metody Action:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

Případně můžete řadič omezit a pak povolit anonymní přístup ke konkrétním akcím pomocí atributu `[AllowAnonymous]`. V následujícím příkladu došlo k omezení metody `Post`, ale metoda `Get` umožňuje anonymní přístup.

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

V předchozích příkladech filtr umožňuje všem ověřeným uživatelům přistupovat k omezeným metodám; jsou zachovány pouze anonymní uživatelé. Přístup můžete také omezit na konkrétní uživatele nebo na uživatele v určitých rolích:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Filtr **AuthorizeAttribute** pro řadiče webového rozhraní API je umístěný v oboru názvů **System. Web. http** . V oboru názvů **System. Web. Mvc** je podobný filtr pro řadiče MVC, což není kompatibilní s řadiči webového rozhraní API.

### <a name="custom-authorization-filters"></a>Vlastní autorizační filtry

Chcete-li napsat vlastní ověřovací filtr, odvozujte jeden z těchto typů:

- **AuthorizeAttribute**. Tuto třídu rozšíříte tak, aby prováděla logiku autorizace na základě aktuálního uživatele a rolí uživatele.
- **AuthorizationFilterAttribute**. Tuto třídu rozšíříte tak, aby prováděla synchronní autorizační logiku, která není nutně založená na aktuálním uživateli nebo roli.
- **IAuthorizationFilter**. Implementujte toto rozhraní, aby se prováděla logika asynchronního ověřování. Například pokud vaše autorizační logika provádí asynchronní vstupně-výstupní operace nebo síťová volání. (Pokud je vaše autorizační logika vázaná na procesor, jednodušší je odvozovat z **AuthorizationFilterAttribute**, protože pak nemusíte psát asynchronní metodu.)

Následující diagram znázorňuje hierarchii tříd pro třídu **AuthorizeAttribute** .

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>Autorizace v rámci akce kontroleru

V některých případech může být možné, že žádost bude pokračovat, ale změní chování na základě objektu zabezpečení. Například vrácené informace se mohou měnit v závislosti na roli uživatele. V rámci metody kontroleru můžete získat aktuální objekt zabezpečení z vlastnosti **ApiController. User** .

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]

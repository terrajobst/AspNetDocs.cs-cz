---
title: Práce s SameSite soubory cookie v ASP.NET
author: rick-anderson
description: Naučte se používat k SameSite souborů cookie v ASP.NET.
ms.author: riande
ms.date: 12/03/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: 40e5c13b6834912c13b41cbfad7da8cd84ca6c8b
ms.sourcegitcommit: 969e7db924ebad3cc0f0cb0d65d148e8b9221b9a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/06/2019
ms.locfileid: "74902022"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>Práce s SameSite soubory cookie v ASP.NET

Podle [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite je koncept [organizace IETF](https://ietf.org/about/) navržený tak, aby poskytoval určitou ochranu proti útokům prostřednictvím CSRF (pro falšování požadavků mezi lokalitami). [Koncept SameSite 2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):

* Ve výchozím nastavení považuje soubory cookie za `SameSite=Lax`.
* Stavy souborů cookie, které explicitně vyhodnotí `SameSite=None`, aby bylo možné povolit doručování mezi weby, by mělo být označeno jako `Secure`.

`Lax` funguje pro většinu souborů cookie aplikace. Některé formy ověřování, jako je [OpenID Connect](https://openid.net/connect/) (OIDC) a [WS-Federation](https://auth0.com/docs/protocols/ws-fed) , jako výchozí vystavení přesměrování na základě. Přesměrování na základě příspěvku spustí ochranu prohlížeče SameSite, takže pro tyto součásti je SameSite zakázaný. Většina přihlášení [OAuth](https://oauth.net/) není ovlivněná kvůli rozdílům ve způsobu, jakým jsou požadavky v toku.

Parametr `None` způsobuje problémy s kompatibilitou s klienty, kteří implementovali předchozí [koncept standard 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (například iOS 12). Viz [Podpora starších prohlížečů](#sob) v tomto dokumentu.

Každá součást ASP.NET Core, která generuje soubory cookie, musí rozhodnout, zda je SameSite vhodná.

## <a name="api-usage-with-samesite"></a>Použití rozhraní API s SameSite

Viz [vlastnost HttpCookie. SameSite.](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)

## <a name="history-and-changes"></a>Historie a změny

Podpora SameSite byla poprvé implementována v .NET 4.7.2 s využitím [konceptu standard 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).

19. listopadu 2019 aktualizace pro Windows aktualizované .NET 4.7.2 + od standardu 2016 až do standardu 2019. Další aktualizace jsou k disdobu pro jiné verze systému Windows. Další informace najdete v následujících KBch:

* [Článek znalostní báze 4531182](https://support.microsoft.com/help/4531182/kb4531182)
* [Článek znalostní báze 4524421](https://support.microsoft.com/help/4524421/kb4524421)

 Koncept 2019 specifikace SameSite:

* Není **zpětně** kompatibilní s konceptem 2016. Další informace najdete v tématu [Podpora starších prohlížečů](#sob) v tomto dokumentu.
* Určuje, že soubory cookie se ve výchozím nastavení považují za `SameSite=Lax`.
* Určuje soubory cookie, které explicitně vyhodnotí `SameSite=None`, aby bylo možné povolit doručování mezi weby, musí být označeno jako `Secure`. `None` je nová položka k odhlášení.
* Je podporován opravami vydanými podle výše uvedených v článku znalostní báze.
* Ve výchozím nastavení je naplánovaná podpora [Chrome](https://chromestatus.com/feature/5088147346030592) v [únoru 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html). Prohlížeče začaly při přesunu do tohoto standardu v 2019.

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>Podpora starších prohlížečů

SameSite standardně vyhodnocuje, že neznámé hodnoty musí být považovány za `SameSite=Strict` hodnoty. 2016 Aplikace, ke kterým se přistupoval ze starších prohlížečů, které podporují SameSite úrovně Standard 2016, se můžou přerušit, když získají vlastnost SameSite s hodnotou `None`. Webové aplikace musí implementovat detekci prohlížeče, pokud chtějí podporovat starší prohlížeče. ASP.NET neimplementuje zjišťování prohlížeče, protože hodnoty uživatelských agentů jsou vysoce těkavé a často se mění. Následující kód lze volat na webu <xref:HTTP.HttpCookie> volání:

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

V předchozí ukázce `MyUserAgentDetectionLib.DisallowsSameSiteNone` je uživatelem zadaná knihovna, která detekuje, jestli Agent pro uživatele nepodporuje SameSite `None`. Následující kód ukazuje ukázkovou `DisallowsSameSiteNone` metodu:

> [!WARNING]
> Následující kód je určen pouze pro ukázku:
> * Neměla by být považována za dokončenou.
> * Není udržována ani podporována.

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>Testování aplikací pro problémy s SameSite

Aplikace, které komunikují se vzdálenými lokalitami, jako je třeba přihlášení třetí strany, potřebují:

* Otestujte interakci na více prohlížečích.
* Použití [zjišťování a zmírnění](#sob) problémů v prohlížeči, které jsou popsány v tomto dokumentu.

Otestujte webové aplikace pomocí verze klienta, která se může přihlásit k novému chování SameSite. Pro Chrome, Firefox a chrom Edge mají všechny nové příznaky funkcí pro výslovný souhlas, které lze použít k testování. Po použití oprav SameSite se aplikace testuje se staršími verzemi klientů, zejména Safari. Další informace najdete v tématu [Podpora starších prohlížečů](#sob) v tomto dokumentu.

### <a name="test-with-chrome"></a>Testování s použitím Chromu

Chrome 78 + poskytuje zavádějící výsledky, protože má na zpracování dočasné omezení. Chrome 78 + dočasné zmírnění umožňuje, aby soubory cookie byly starší než dvě minuty. Chrome 76 nebo 77 s povolenými vhodnými příznakem testu poskytuje přesnější výsledky. Chcete-li otestovat nové chování SameSite, přepněte `chrome://flags/#same-site-by-default-cookies` na **povoleno**. Starší verze Chrome (75 a novější) jsou hlášeny jako neúspěšné s novým nastavením `None`. Viz [Podpora starších prohlížečů](#sob) v tomto dokumentu.

Google nezpřístupňuje starší verze Chrome. Postupujte podle pokynů v části [stažení Chromu](https://www.chromium.org/getting-involved/download-chromium) a otestujte starší verze Chrome. Nestahujte Chrome z odkazů **, které jsou** k dispozici, hledáním ve starších verzích Chrome.

* [Chróm 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chróm 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>Testování pomocí Safari

Prohlížeč Safari 12 striktně implementuje předchozí koncept a v případě, že je nová hodnota `None` v souboru cookie, se nezdařila. `None` se vyhnete prostřednictvím kódu detekce prohlížeče, který [podporuje starší prohlížeče](#sob) v tomto dokumentu. Pomocí MSAL, ADAL nebo libovolné knihovny, kterou používáte, otestujte přihlašovací údaje pro WebKit Safari 12, Safari 13 a na bázi. Problém závisí na základní verzi operačního systému. OSX Mojave (10,14) a iOS 12 se nazývají problémy s kompatibilitou s novým chováním SameSite. Upgrade operačního systému na OSX Catalina (10,15) nebo iOS 13 opravuje problém. Prohlížeč Safari aktuálně nemá příznak výslovných přihlášení pro testování nového chování specifikace.

### <a name="test-with-firefox"></a>Testování pomocí Firefox

Podporu aplikace Firefox pro nový standard lze testovat na verzi 68 + tím, že na stránce `about:config` `network.cookie.sameSite.laxByDefault`příznak funkce. Nebyly zjištěny žádné zprávy o problémech s kompatibilitou se staršími verzemi aplikace Firefox.

### <a name="test-with-edge-browser"></a>Testování pomocí prohlížeče Edge

Edge podporuje starý SameSite Standard. Edge verze 44 nemá žádné známé problémy s kompatibilitou s novým standardem.

### <a name="test-with-edge-chromium"></a>Test s hranou (chrom)

Příznaky SameSite jsou nastaveny na stránce `edge://flags/#same-site-by-default-cookies`. U Edge Chromu se nezjistily žádné problémy s kompatibilitou.

### <a name="test-with-electron"></a>Testování s elektronem

K verzím elektronů patří starší verze Chromu. Například verze elektronicky používané týmy je chrom 66, který vykazuje starší chování. Je nutné provést vlastní testování kompatibility s verzí elektronů, kterou váš produkt používá. Viz [Podpora starších prohlížečů](#sob) v následující části.

## <a name="additional-resources"></a>Další materiály a zdroje informací

* [Chromový blog: vývojáři: Připravte se na nové SameSite = None; Nastavení zabezpečeného souboru cookie](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Vysvětlení souborů cookie SameSite](https://web.dev/samesite-cookies-explained/)

---
title: Práce s SameSite soubory cookie a otevřeným webovým rozhraním pro .NET (OWIN)
author: rick-anderson
description: Práce s SameSite soubory cookie a otevřeným webovým rozhraním pro .NET (OWIN)
ms.author: riande
ms.date: 12/6/2019
uid: owin-samesite
ms.openlocfilehash: ac5ae24eeb9e8e1cc6296667a4bebef72c3eb62c
ms.sourcegitcommit: 7b1e1784213dd4c301635f9e181764f3e2f94162
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/10/2019
ms.locfileid: "74993073"
---
# <a name="samesite-cookies-and-the-open-web-interface-for-net-owin"></a>SameSite soubory cookie a otevřené webové rozhraní pro .NET (OWIN)

Podle [Rick Anderson](https://twitter.com/RickAndMSFT)

`SameSite` je koncept [organizace IETF](https://ietf.org/about/) navržený tak, aby poskytoval určitou ochranu proti útokům přes CSRF (mezi lokalitami). [Koncept SameSite 2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):

* Ve výchozím nastavení považuje soubory cookie za `SameSite=Lax`.
* Stavy souborů cookie, které explicitně vyhodnotí `SameSite=None`, aby bylo možné povolit doručování mezi weby, by mělo být označeno jako `Secure`.

`Lax` funguje pro většinu souborů cookie aplikace. Některé formy ověřování, jako je [OpenID Connect](https://openid.net/connect/) (OIDC) a [WS-Federation](https://auth0.com/docs/protocols/ws-fed) , jako výchozí vystavení přesměrování na základě. Přesměrování na základě příspěvku spustí `SameSite` ochrany prohlížečem, takže `SameSite` pro tyto součásti zakázáno. Většina přihlášení [OAuth](https://oauth.net/) není ovlivněná kvůli rozdílům ve způsobu, jakým jsou požadavky v toku. Všechny ostatní komponenty ve **výchozím nastavení nenastaví `SameSite`** a používají výchozí chování klientů (staré nebo nové).

Parametr `None` způsobuje problémy s kompatibilitou s klienty, kteří implementovali předchozí [koncept standard 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (například iOS 12). Viz [Podpora starších prohlížečů](#sob) v tomto dokumentu.

Každá komponenta OWIN, která generuje soubory cookie, musí rozhodnout, zda je `SameSite` vhodné.

Verzi tohoto článku pro ASP.NET 4. x najdete v tématu <xref:samesite/system-web-samesite>.

## <a name="api-usage-with-samesite"></a>Použití rozhraní API s SameSite

`Microsoft.Owin` má vlastní `SameSite` implementaci:

* Ta není přímo závislá na `System.Web`.
* `SameSite` funguje na všech verzích, které cílí na `Microsoft.Owin` balíčky, .NET 4,5 a novější.
* Pouze komponenta [SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs) přímo spolupracuje s třídou `System.Web` `HttpCookie`.

`SystemWebCookieManager` závisí na rozhraních API .NET 4.7.2 `System.Web` pro povolení `SameSite` podpory a opravách, které mění chování.

Důvody pro použití `SystemWebCookieManager` jsou popsaných v [potížích s integrací souborů cookie Owin a System. Web Response](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues). `SystemWebCookieManager` se doporučuje při spuštění v `System.Web`.

Následující sady kódů `SameSite` `Lax`:

```csharp
owinContext.Response.Cookies.Append("My Key", "My Value", new CookieOptions()
{
    SameSite = SameSiteMode.Lax
});
```

Následující rozhraní API používají `SameSite`:

* [Microsoft. Owin. SameSiteMode](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin/SameSiteMode.cs)
* [CookieOptions.SameSite](xref:Microsoft.AspNetCore.Http.CookieOptions.SameSite)
* [CookieAuthenticationOptions – třída](/previous-versions/aspnet/dn385599(v%3Dvs.113)) <!-- CookieAuthenticationOptions.CookieSameSite not published -->
* [CookieAuthenticationOptions.CookieSameSite](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L68-#L72)
* [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113))
* [SystemWebCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebCookieManager.cs)
* [SystemWebChunkingCookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Host.SystemWeb/SystemWebChunkingCookieManager.cs)
* [CookieAuthenticationOptions.CookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.Cookies/CookieAuthenticationOptions.cs#L143-#AL148)
* [OpenIdConnectAuthenticationOptions.CookieManager](https://github.com/aspnet/AspNetKatana/blob/dev/src/Microsoft.Owin.Security.OpenIdConnect/OpenIdConnectAuthenticationOptions.cs#L315-#L318)

## <a name="history-and-changes"></a>Historie a změny

[Microsoft. Owin](https://www.nuget.org/packages/Microsoft.Owin/) nikdy nepodporuje [koncept Standard`SameSite` 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).

Podpora [konceptu SameSite 2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) je k dispozici pouze v `Microsoft.Owin` 4.1.0 a novějších. Pro předchozí verze nejsou k dispozici žádné opravy.

Koncept 2019 specifikace `SameSite`:

* Není **zpětně** kompatibilní s konceptem 2016. Další informace najdete v tématu [Podpora starších prohlížečů](#sob) v tomto dokumentu.
* Určuje, že soubory cookie se ve výchozím nastavení považují za `SameSite=Lax`.
* Určuje soubory cookie, které explicitně vyhodnotí `SameSite=None`, aby bylo možné povolit doručování mezi weby, musí být označeno jako `Secure`. `None` je nová položka k odhlášení.
* Ve výchozím nastavení je naplánovaná podpora [Chrome](https://chromestatus.com/feature/5088147346030592) v [únoru 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html). Prohlížeče začaly při přesunu do tohoto standardu v 2019.
* Je podporován opravami vydanými podle pokynů v článcích znalostní báze. Další informace najdete v tématu <xref:samesite/kbs-samesite>.

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>Podpora starších prohlížečů

2016 `SameSite` standardně posuzuje, že neznámé hodnoty musí být považovány za `SameSite=Strict` hodnoty. Aplikace, ke kterým se přistupoval ze starších prohlížečů, které podporují 2016 `SameSite` Standard, se můžou přerušit, když získají vlastnost `SameSite` s hodnotou `None`. Webové aplikace musí implementovat detekci prohlížeče, pokud chtějí podporovat starší prohlížeče. ASP.NET neimplementuje zjišťování prohlížeče, protože hodnoty uživatelských agentů jsou vysoce těkavé a často se mění. Bod rozšíření v [ICookieManager](/previous-versions/aspnet/dn800238(v%3Dvs.113)) umožňuje zapojení do logiky specifické pro uživatele.
<!-- https://docs.microsoft.com/en-us/previous-versions/aspnet/dn800238(v%3Dvs.113) -->

V `Startup.Configuration`přidejte kód podobný následujícímu:

[!code-csharp[](sample/Startup1.cs?name=snippet)]

Předchozí kód vyžaduje rozhraní .NET 4.7.2 nebo novější opravu `SameSite`.

Následující kód ukazuje příklad implementace `SameSiteCookieManager`:

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet)]

V předchozím příkladu je `DisallowsSameSiteNone` volána v metodě `CheckSameSite`. `DisallowsSameSiteNone` je metoda uživatele, která zjistí, zda uživatelský agent nepodporuje `SameSite` `None`:

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet3&highlight=4)]

Následující kód ukazuje ukázkovou `DisallowsSameSiteNone` metodu:

> [!WARNING]
> Následující kód je určen pouze pro ukázku:
> * Neměla by být považována za dokončenou.
> * Není udržována ani podporována.

[!code-csharp[](sample/SameSiteCookieManager.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a>Testování aplikací pro problémy s SameSite

Aplikace, které komunikují se vzdálenými lokalitami, jako je třeba přihlášení třetí strany, potřebují:

* Otestujte interakci na více prohlížečích.
* Použití [zjišťování a zmírnění](#sob) problémů v prohlížeči, které jsou popsány v tomto dokumentu.

Otestujte webové aplikace pomocí verze klienta, která se může přihlásit k novému chování `SameSite`. Pro Chrome, Firefox a chrom Edge mají všechny nové příznaky funkcí pro výslovný souhlas, které lze použít k testování. Jakmile vaše aplikace použije `SameSite` opravy, otestujte ji pomocí starších verzí klientů, zejména Safari. Další informace najdete v tématu [Podpora starších prohlížečů](#sob) v tomto dokumentu.

### <a name="test-with-chrome"></a>Testování s použitím Chromu

Chrome 78 + poskytuje zavádějící výsledky, protože má na zpracování dočasné omezení. Chrome 78 + dočasné zmírnění umožňuje, aby soubory cookie byly starší než dvě minuty. Chrome 76 nebo 77 s povolenými vhodnými příznakem testu poskytuje přesnější výsledky. Chcete-li otestovat nové rozhraní `SameSite` přepínač chování je `chrome://flags/#same-site-by-default-cookies` **povoleno**. Starší verze Chrome (75 a novější) jsou hlášeny jako neúspěšné s novým nastavením `None`. Viz [Podpora starších prohlížečů](#sob) v tomto dokumentu.

Google nezpřístupňuje starší verze Chrome. Postupujte podle pokynů v části [stažení Chromu](https://www.chromium.org/getting-involved/download-chromium) a otestujte starší verze Chrome. Nestahujte Chrome z odkazů **, které jsou** k dispozici, hledáním ve starších verzích Chrome.

* [Chróm 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chróm 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a>Testování pomocí Safari

Prohlížeč Safari 12 striktně implementuje předchozí koncept a v případě, že je nová hodnota `None` v souboru cookie, se nezdařila. `None` se vyhnete prostřednictvím kódu detekce prohlížeče, který [podporuje starší prohlížeče](#sob) v tomto dokumentu. Pomocí MSAL, ADAL nebo libovolné knihovny, kterou používáte, otestujte přihlašovací údaje pro WebKit Safari 12, Safari 13 a na bázi. Problém závisí na základní verzi operačního systému. OSX Mojave (10,14) a iOS 12 se nazývají problémy s kompatibilitou s novým chováním `SameSite`. Upgrade operačního systému na OSX Catalina (10,15) nebo iOS 13 opravuje problém. Prohlížeč Safari aktuálně nemá příznak výslovných přihlášení pro testování nového chování specifikace.

### <a name="test-with-firefox"></a>Testování pomocí Firefox

Podporu aplikace Firefox pro nový standard lze testovat na verzi 68 + tím, že na stránce `about:config` `network.cookie.sameSite.laxByDefault`příznak funkce. Nebyly zjištěny žádné zprávy o problémech s kompatibilitou se staršími verzemi aplikace Firefox.

### <a name="test-with-edge-browser"></a>Testování pomocí prohlížeče Edge

Edge podporuje starý `SameSite` Standard. Edge verze 44 nemá žádné známé problémy s kompatibilitou s novým standardem.

### <a name="test-with-edge-chromium"></a>Test s hranou (chrom)

příznaky `SameSite` jsou nastaveny na stránce `edge://flags/#same-site-by-default-cookies`. U Edge Chromu se nezjistily žádné problémy s kompatibilitou.

### <a name="test-with-electron"></a>Testování s elektronem

K verzím elektronů patří starší verze Chromu. Například verze elektronicky používané týmy je chrom 66, který vykazuje starší chování. Je nutné provést vlastní testování kompatibility s verzí elektronů, kterou váš produkt používá. Viz [Podpora starších prohlížečů](#sob) v následující části.

## <a name="additional-resources"></a>Další materiály a zdroje informací

* [Chromový blog: vývojáři: Připravte se na nové SameSite = None; Nastavení zabezpečeného souboru cookie](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Vysvětlení souborů cookie SameSite](https://web.dev/samesite-cookies-explained/)
* [Problémy s integrací souboru cookie OWIN a System. Web Response](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues)

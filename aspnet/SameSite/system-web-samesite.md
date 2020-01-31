---
title: Práce s SameSite soubory cookie v ASP.NET
author: rick-anderson
description: Naučte se používat k SameSite souborů cookie v ASP.NET.
ms.author: riande
ms.date: 1/22/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: c81ca38648609aa5347d2a8cc11889fc85d81711
ms.sourcegitcommit: 4d439e01c82c7c95b19216fedaf5b1a11a1deb06
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76826611"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>Práce s SameSite soubory cookie v ASP.NET

Podle [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite je Konceptový standard [IETF](https://ietf.org/about/) navržený tak, aby poskytoval určitou ochranu proti útokům prostřednictvím CSRF (pro falšování požadavků mezi lokalitami). Původně koncept v [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)se aktualizoval koncept standardu v [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00). Aktualizovaný Standard není zpětně kompatibilní s předchozím standardem, přičemž následující je největší znatelné rozdíly:

* Soubory cookie bez hlavičky SameSite se ve výchozím nastavení považují za `SameSite=Lax`.
* aby bylo možné používat soubory cookie pro více webů, je třeba použít `SameSite=None`.
* Soubory cookie, které vyhodnotí `SameSite=None`, musí být také označeny jako `Secure`.
* Hodnota SameSite = None není povolena [standardem 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07) a způsobí, že některé implementace považují takové soubory cookie za SameSite = Strict. Viz [Podpora starších prohlížečů](#sob) v tomto dokumentu.

Nastavení `SameSite=Lax` funguje pro většinu souborů cookie aplikace. Některé formy ověřování, jako je [OpenID Connect](https://openid.net/connect/) (OIDC) a [WS-Federation](https://auth0.com/docs/protocols/ws-fed) , jako výchozí vystavení přesměrování na základě. Přesměrování na základě příspěvku spustí ochranu prohlížeče SameSite, takže pro tyto součásti je SameSite zakázaný. Většina přihlášení [OAuth](https://oauth.net/) není ovlivněná kvůli rozdílům ve způsobu, jakým jsou požadavky v toku.

U aplikací, které používají `iframe`, může docházet k potížím s `SameSite=Lax` nebo `SameSite=Strict` soubory cookie, protože prvky IFrame jsou považovány za scénáře mezi weby.

Každá komponenta ASP.NET, která generuje soubory cookie, musí rozhodnout, zda je SameSite vhodná.

Informace o problémech s aplikacemi po instalaci aktualizací 2019 .NET SameSite najdete v tématu [známé problémy](#known) .

## <a name="using-samesite-in-aspnet-472-and-48"></a>Použití SameSite v ASP.NET 4.7.2 a 4,8

.NET 4.7.2 a 4,8 podporují [koncept standard 2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) pro SameSite od vydání aktualizací v prosinci 2019. Vývojáři mohou programově řídit hodnotu hlavičky SameSite pomocí [vlastnosti HttpCookie. SameSite](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite). Nastavení vlastnosti `SameSite` na `Strict`, `Lax`nebo `None` výsledky v těchto hodnotách, které jsou v síti zapisovány pomocí souboru cookie. Nastavení rovno `(SameSiteMode)(-1)` znamená, že v síti se souborem cookie by neměl být zahrnutá hlavička SameSite. [Vlastnost HttpCookie. Secure](/dotnet/api/system.web.httpcookie.secure)nebo ' vlastnost requireSSL ' v konfiguračních souborech lze použít k označení souboru cookie jako `Secure` nebo ne.

Nové instance `HttpCookie` budou ve výchozím nastavení `SameSite=(SameSiteMode)(-1)` a `Secure=false`. Tato výchozí nastavení se dají přepsat v konfigurační sekci `system.web/httpCookies`, kde řetězec `"Unspecified"` je uživatelsky přívětivou syntaxí pro `(SameSiteMode)(-1)`, která je jenom pro konfiguraci.

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

ASP.Net také pro tyto funkce vydává čtyři konkrétní soubory cookie vlastní: anonymní ověřování, ověřování formulářů, stav relace a Správa rolí. Instance těchto souborů cookie, které jsou získány v modulu runtime, mohou být manipulovány pomocí `SameSite` a `Secure` vlastností stejně jako jakékoli jiné instance HttpCookie. V důsledku patchworkí SameSite Standard se ale možnosti konfigurace pro tyto čtyři soubory cookie neshodují. Příslušné konfigurační oddíly a atributy s výchozími hodnotami jsou uvedeny níže. Pokud není k dispozici žádný `SameSite` nebo `Secure` v atributu pro funkci, pak se tato funkce přepne na výchozí hodnoty nakonfigurované v části `system.web/httpCookies` popsané výše.

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequiresSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**Poznámka**: možnost Neurčeno je k dispozici pouze pro `system.web/httpCookies@sameSite` v daném okamžiku. Doufáme, že přidáte podobnou syntaxi k dříve zobrazeným atributům cookieSameSite v budoucích aktualizacích. Nastavení `(SameSiteMode)(-1)` v kódu pořád funguje na instancích těchto souborů cookie. *

## <a name="history-and-changes"></a>Historie a změny

Podpora SameSite byla poprvé implementována v .NET 4.7.2 s využitím [konceptu standard 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).

19. listopadu 2019 aktualizace pro Windows aktualizované .NET 4.7.2 + od standardu 2016 až do standardu 2019. Další aktualizace jsou k disdobu pro jiné verze systému Windows. Další informace najdete v tématu <xref:samesite/kbs-samesite>.

 Koncept 2019 specifikace SameSite:

* Není **zpětně** kompatibilní s konceptem 2016. Další informace najdete v tématu [Podpora starších prohlížečů](#sob) v tomto dokumentu.
* Určuje, že soubory cookie se ve výchozím nastavení považují za `SameSite=Lax`.
* Určuje soubory cookie, které explicitně vyhodnotí `SameSite=None`, aby bylo možné povolit doručování mezi weby, musí být označeno jako `Secure`.
* Je podporován opravami vydanými podle výše uvedených v článku znalostní báze.
* Ve výchozím nastavení je naplánovaná podpora [Chrome](https://chromestatus.com/feature/5088147346030592) v [únoru 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html). Prohlížeče začaly při přesunu do tohoto standardu v 2019.

<a name="known"><a/>

## <a name="known-issues"></a>Známé problémy

Vzhledem k tomu, že specifikace konceptu 2016 a 2019 nejsou kompatibilní, aktualizace 2019 pro rozhraní .NET Framework zavádí některé změny, které mohou být přerušují.

* Soubory cookie pro ověření stavu relace a formulářů jsou nyní zapisovány do sítě, protože místo nespecifikovaného je `Lax`.
  * I když většina aplikací spolupracuje s `SameSite=Lax` soubory cookie, aplikace, které odesílají weby nebo aplikace, které využívají `iframe`, můžou zjistit, že se jejich stav relace nebo soubory cookie autorizace formulářů nepoužívají podle očekávání. Pokud to chcete napravit, změňte hodnotu `cookieSameSite` v příslušném konfiguračním oddílu, jak je popsáno výše.
* HttpCookies, který explicitně nastaví `SameSite=None` v kódu nebo v konfiguraci, má nyní tuto hodnotu napsanou v souboru cookie, zatímco dříve byla vynechána. To může způsobit problémy se staršími prohlížeči, které podporují jenom 2016 koncept Standard.
  * Když cílíte na prohlížeče, které podporují pracovní Standard 2019 s `SameSite=None` soubory cookie, nezapomeňte je také označit `Secure` nebo nemusejí být rozpoznány.
  * Pokud se chcete vrátit k 2016 chování, které nepíše `SameSite=None`, použijte nastavení aplikace `aspnet:SupressSameSiteNone=true`. Všimněte si, že tato akce bude platit pro všechny HttpCookies v aplikaci.

### <a name="azure-app-servicesamesite-cookie-handling"></a>Azure App Service – zpracování souborů cookie SameSite

Informace o tom, jak Azure App Service konfiguruje chování SameSite v aplikacích .NET 4.7.2, najdete v tématu [Azure App Service – zpracování souborů cookie SameSite a .NET Framework opravy 4.7.2](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) .

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

* [Nadcházející změny souborů cookie SameSite v ASP.NET a ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Chromový blog: vývojáři: Připravte se na nové SameSite = None; Nastavení zabezpečeného souboru cookie](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Vysvětlení souborů cookie SameSite](https://web.dev/samesite-cookies-explained/)

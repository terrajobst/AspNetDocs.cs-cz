---
title: Práce s SameSite soubory cookie v ASP.NET
author: rick-anderson
description: Naučte se používat k SameSite souborů cookie v ASP.NET.
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: edb368910b24be2d042afe3c19ffa1fb23245443
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455699"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>Práce s SameSite soubory cookie v ASP.NET

Autor: [Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite je Konceptový standard [IETF](https://ietf.org/about/) navržený tak, aby poskytoval určitou ochranu proti útokům prostřednictvím CSRF (pro falšování požadavků mezi lokalitami). Původně koncept v [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)se aktualizoval koncept standardu v [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00). Aktualizovaný Standard není zpětně kompatibilní s předchozím standardem, přičemž následující je největší znatelné rozdíly:

* Soubory cookie bez hlavičky SameSite se ve výchozím nastavení považují za `SameSite=Lax`.
* aby bylo možné používat soubory cookie pro více webů, je třeba použít `SameSite=None`.
* Soubory cookie, které vyhodnotí `SameSite=None`, musí být také označeny jako `Secure`.
* U aplikací, které používají [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) , může docházet k problémům s `sameSite=Lax` nebo `sameSite=Strict` soubory cookie, protože `<iframe>` se považují za scénáře mezi lokalitami.
* Hodnota `SameSite=None` není povolena [standardem 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07) a způsobí, že některé implementace považují takové soubory cookie za `SameSite=Strict`. Viz [Podpora starších prohlížečů](#sob) v tomto dokumentu.

Nastavení `SameSite=Lax` funguje pro většinu souborů cookie aplikace. Některé formy ověřování, jako je [OpenID Connect](https://openid.net/connect/) (OIDC) a [WS-Federation](https://auth0.com/docs/protocols/ws-fed) , jako výchozí vystavení přesměrování na základě. Přesměrování na základě příspěvku spustí ochranu prohlížeče SameSite, takže pro tyto součásti je SameSite zakázaný. Většina přihlášení [OAuth](https://oauth.net/) není ovlivněná kvůli rozdílům ve způsobu, jakým jsou požadavky v toku.

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
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**Poznámka**: možnost Neurčeno je k dispozici pouze pro `system.web/httpCookies@sameSite` v daném okamžiku. Doufáme, že přidáte podobnou syntaxi k dříve zobrazeným atributům cookieSameSite v budoucích aktualizacích. Nastavení `(SameSiteMode)(-1)` v kódu pořád funguje na instancích těchto souborů cookie. *

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a>Změna cílení aplikací .NET

Pro cílení na .NET 4.7.2 nebo novější:

* Zajistěte, aby soubor *Web. config* obsahoval následující:  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  Další podrobnosti najdete v [příručce k migraci rozhraní .NET](/dotnet/framework/migration-guide/) .

* Ověřte, jestli jsou balíčky NuGet v projektu cílené na správnou verzi rozhraní .NET Framework. Správnou verzi rozhraní můžete ověřit kontrolou souboru *Packages. config* , například:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  V předchozím souboru *Packages. config* se `Microsoft.ApplicationInsights` balíčku:
    * Je zaměřený na rozhraní .NET 4.5.1.
    * Měla by mít atribut `targetFramework` aktualizován tak, aby `net472`, pokud existuje aktualizovaný balíček cílený na váš cílový rámec.

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a>Verze rozhraní .NET starší než 4.7.2

Společnost Microsoft nepodporuje verze .NET nižší, než 4.7.2 pro zápis atributu souboru cookie stejné lokality. Nejsme nenašli spolehlivý způsob, jak:

* Ujistěte se, že je správně napsaný atribut na základě verze prohlížeče.
* Zachycujte a upravujete soubory cookie ověřování a relací ve starších verzích rozhraní.

### <a name="december-patch-behavior-changes"></a>Prosince změny chování opravy

Konkrétní změnou chování pro .NET Framework je způsob, jakým vlastnost `SameSite` interpretuje hodnotu `None`:

* Před opravou hodnoty `None` určena:
  * Negenerovat atribut vůbec.
* Po opravě:
  * Hodnota `None`znamená "vygenerovat atribut s hodnotou `None`".
  * Hodnota `SameSite` `(SameSiteMode)(-1)` způsobí, že se atribut neemituje.

Výchozí hodnota SameSite pro ověřování pomocí formulářů a soubory cookie stavu relace se změnila z `None` na `Lax`.

### <a name="summary-of-change-impact-on-browsers"></a>Shrnutí dopadu na změnu v prohlížečích

Pokud nainstalujete opravu a vydáte soubor cookie s `SameSite.None`, dojde k jedné ze dvou akcí:
* V80 Chrome tento soubor cookie zachová podle nové implementace a neuplatní pro tento soubor cookie stejná omezení webu.
* Všechny prohlížeče, které nebyly aktualizovány pro podporu nové implementace, budou následovat po původní implementaci. Stará implementace říká:
  * Pokud se vám zobrazí hodnota, kterou nerozumíte, ignorujte ji a přepněte na přísná omezení lokalit.

Takže se aplikace buď poruší, nebo dojde k přerušení na mnoha dalších místech.

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

SameSite standardně vyhodnocuje, že neznámé hodnoty musí být považovány za `SameSite=Strict` hodnoty. 2016 Aplikace, ke kterým se přistupoval ze starších prohlížečů, které podporují SameSite úrovně Standard 2016, se můžou přerušit, když získají vlastnost SameSite s hodnotou `None`. Webové aplikace musí implementovat detekci prohlížeče, pokud chtějí podporovat starší prohlížeče. ASP.NET neimplementuje zjišťování prohlížeče, protože hodnoty uživatelských agentů jsou vysoce těkavé a často se mění.

Přístup společnosti Microsoft k řešení problému vám usnadní implementaci komponent detekce prohlížeče, aby bylo možné z souborů cookie nakládat atribut `sameSite=None`, pokud je známo, že ho prohlížeč nepodporují. Při poradenství od společnosti Google bylo nutné vystavit dvojité soubory cookie, jeden s novým atributem a druhý bez atributu. Doporučujeme však, abyste považovat jenom na Rady Google. Některé prohlížeče, zejména mobilní prohlížeče, mají velmi malá omezení počtu souborů cookie, které web nebo název domény může odeslat. Odesílání více souborů cookie, zejména velkých souborů cookie, jako jsou soubory cookie pro ověřování, může dosáhnout vysokého limitu, což způsobí selhání aplikací, které je obtížné diagnostikovat a opravovat. Kromě architektury existuje velký ekosystém kódu a komponent třetích stran, které nemusejí být aktualizovány, aby používaly přístup pomocí dvojitých souborů cookie.

Kód pro detekci prohlížeče použitý v ukázkových projektech v [tomto úložišti GitHubu]() je obsažen ve dvou souborech.

* [C#SameSiteSupport.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [VB SameSiteSupport. vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

Tyto detekce jsou nejběžnějšími agenty prohlížeče, kteří viděli, že podporují Standard 2016 a pro které je potřeba atribut úplně odebrat. Není určena jako kompletní implementace:

* Vaše aplikace může zobrazit prohlížeče, které naše testovací weby nepodporují.
* Měli byste být připraveni přidat detekce podle potřeby vašeho prostředí.

Způsob, jakým se detekuje detekce, se liší podle verze rozhraní .NET a webového rozhraní, které používáte. Následující kód lze volat na webu <xref:HTTP.HttpCookie> volání:

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

Podívejte se na následující témata ASP.NET souborů cookie 4.7.2 SameSite:

* [C#NÁVRHOVÝ](xref:samesite/csMVC)
* [C#Webových formulářů](xref:samesite/CSharpWebForms)
* [Webforma VB](xref:samesite/vbWF)
* [VB MVC](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a>Zajištění přesměrování lokality na HTTPS

Pro přesměrování všech požadavků na protokol HTTPS se dá použít funkce pro [přepsání adresy URL služby](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) ASP.NET 4. x, WebForms a MVC. Následující kód XML ukazuje vzorové pravidlo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

V místních instalacích opětovného [zápisu adres URL IIS](https://www.iis.net/downloads/microsoft/url-rewrite) je volitelná funkce, která může být potřeba nainstalovat.

## <a name="test-apps-for-samesite-problems"></a>Testování aplikací pro problémy s SameSite

Aplikaci musíte otestovat pomocí prohlížečů, které podporujete, a Projděte si scénáře, které zahrnují soubory cookie. Scénáře souborů cookie obvykle zahrnují

* Formuláře pro přihlášení
* Externí mechanismy přihlášení, jako je Facebook, Azure AD, OAuth a OIDC
* Stránky, které přijímají žádosti z jiných lokalit
* Stránky v aplikaci navržené tak, aby byly vložené v iFrames

Měli byste kontrolovat, jestli jsou soubory cookie vytvořené, trvalé a odstraněné ve vaší aplikaci správně.

Aplikace, které komunikují se vzdálenými lokalitami, jako je třeba přihlášení třetí strany, potřebují:

* Otestujte interakci na více prohlížečích.
* Použití [zjišťování a zmírnění](#sob) problémů v prohlížeči, které jsou popsány v tomto dokumentu.

Otestujte webové aplikace pomocí verze klienta, která se může přihlásit k novému chování SameSite. Pro Chrome, Firefox a chrom Edge mají všechny nové příznaky funkcí pro výslovný souhlas, které lze použít k testování. Po použití oprav SameSite se aplikace testuje se staršími verzemi klientů, zejména Safari. Další informace najdete v tématu [Podpora starších prohlížečů](#sob) v tomto dokumentu.

### <a name="test-with-chrome"></a>Testování s použitím Chromu

Chrome 78 + poskytuje zavádějící výsledky, protože má na zpracování dočasné omezení. Chrome 78 + dočasné zmírnění umožňuje, aby soubory cookie byly starší než dvě minuty. Chrome 76 nebo 77 s povolenými vhodnými příznakem testu poskytuje přesnější výsledky. Chcete-li otestovat nové chování SameSite, přepněte `chrome://flags/#same-site-by-default-cookies` na **povoleno**. Starší verze Chrome (75 a novější) jsou hlášeny jako neúspěšné s novým nastavením `None`. Viz [Podpora starších prohlížečů](#sob) v tomto dokumentu.

Google nezpřístupňuje starší verze Chrome. Postupujte podle pokynů v části [stažení Chromu](https://www.chromium.org/getting-involved/download-chromium) a otestujte starší verze Chrome. Nestahujte Chrome z odkazů **, které jsou** k dispozici, hledáním ve starších verzích Chrome.

* [Chróm 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chróm 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* Pokud nepoužíváte 64bitovou verzi systému Windows, můžete pomocí [prohlížeče OmahaProxy](https://omahaproxy.appspot.com/) vyhledat, která větev Chromu odpovídá stylu Chrome 74 (v 74.0.3729.108), a to podle [pokynů uvedených v Chromu](https://www.chromium.org/getting-involved/download-chromium).

#### <a name="test-with-chrome-80"></a>Testování s použitím Chromu 80 +

[Stáhněte si](https://www.google.com/chrome/) verzi Chrome, která podporuje jejich nový atribut. V době psaní je aktuální verze Chrome 80. Chrome 80 vyžaduje, aby byl příznak `chrome://flags/#same-site-by-default-cookies` povolen pro použití nového chování. Měli byste taky povolit (`chrome://flags/#cookies-without-same-site-must-be-secure`) pro otestování nadcházejícího chování souborů cookie, u kterých není povolený žádný atribut sameSite. Chrome 80 je v cíli, aby tento přepínač považoval soubory cookie bez atributu `SameSite=Lax`, i když s časovým obdobím pro určité žádosti. Chcete-li zakázat časový limit doby odkladu, je možné spustit Chrome 80 s následujícím argumentem příkazového řádku:

`--enable-features=SameSiteDefaultChecksMethodRigorously`

Chrome 80 obsahuje varovné zprávy v konzole prohlížeče o chybějících atributech sameSite. Pomocí F12 otevřete konzolu prohlížeče.

### <a name="test-with-safari"></a>Testování pomocí Safari

Prohlížeč Safari 12 striktně implementuje předchozí koncept a v případě, že je nová hodnota `None` v souboru cookie, se nezdařila. `None` se vyhnete prostřednictvím kódu detekce prohlížeče, který [podporuje starší prohlížeče](#sob) v tomto dokumentu. Pomocí MSAL, ADAL nebo libovolné knihovny, kterou používáte, otestujte přihlašovací údaje pro WebKit Safari 12, Safari 13 a na bázi. Problém závisí na základní verzi operačního systému. OSX Mojave (10,14) a iOS 12 se nazývají problémy s kompatibilitou s novým chováním SameSite. Upgrade operačního systému na OSX Catalina (10,15) nebo iOS 13 opravuje problém. Prohlížeč Safari aktuálně nemá příznak výslovných přihlášení pro testování nového chování specifikace.

### <a name="test-with-firefox"></a>Testování pomocí Firefox

Podporu aplikace Firefox pro nový standard lze testovat na verzi 68 + tím, že na stránce `about:config` `network.cookie.sameSite.laxByDefault`příznak funkce. Nebyly zjištěny žádné zprávy o problémech s kompatibilitou se staršími verzemi aplikace Firefox.

### <a name="test-with-edge-legacy-browser"></a>Test pomocí prohlížeče Microsoft Edge (starší verze)

Edge podporuje starý SameSite Standard. Edge verze 44 + nemá žádné známé problémy s kompatibilitou s novým standardem.

### <a name="test-with-edge-chromium"></a>Test s hranou (chrom)

Příznaky SameSite jsou nastaveny na stránce `edge://flags/#same-site-by-default-cookies`. U Edge Chromu se nezjistily žádné problémy s kompatibilitou.

### <a name="test-with-electron"></a>Testování s elektronem

K verzím elektronů patří starší verze Chromu. Například verze elektronicky používané týmy je chrom 66, který vykazuje starší chování. Je nutné provést vlastní testování kompatibility s verzí elektronů, kterou váš produkt používá. Viz [Podpora starších prohlížečů](#sob).

## <a name="reverting-samesite-patches"></a>Vracení SameSite oprav

Můžete obnovit aktualizované chování sameSite v aplikaci .NET Framework aplikace na předchozí chování, kde atribut sameSite není generován pro hodnotu `None`a vrátit soubory cookie ověřování a relace, aby negenerovaly hodnotu. Tato akce by se měla zobrazit jako *extrémně dočasná oprava*, protože změny v Chromu přeruší všechny požadavky externích příspěvků nebo ověřování pro uživatele pomocí prohlížečů, které podporují změny standardu.

### <a name="reverting-net-472-behavior"></a>Vrácení chování .NET 4.7.2

Aktualizujte soubor *Web. config* tak, aby zahrnoval následující nastavení konfigurace:

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a>Další materiály a zdroje informací

* [Nadcházející změny souborů cookie SameSite v ASP.NET a ASP.NET Core](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [Chromový blog: vývojáři: Připravte se na nové SameSite = None; Nastavení zabezpečeného souboru cookie](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [Vysvětlení souborů cookie SameSite](https://web.dev/samesite-cookies-explained/)
* [Aktualizace pro Chrome](https://www.chromium.org/updates/same-site)
* [Opravy .NET SameSite](/aspnet/samesite/kbs-samesite)
* [Informace o stejných lokalitách webových aplikací Azure](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [Informace o stejných lokalitách Azure Active Directory](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)

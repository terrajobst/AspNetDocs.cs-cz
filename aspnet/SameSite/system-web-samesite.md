---
title: Práce s SameSite soubory cookie v ASP.NET
author: rick-anderson
description: Naučte se používat k SameSite souborů cookie v ASP.NET.
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: edb368910b24be2d042afe3c19ffa1fb23245443
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455699"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="1ca4f-103">Práce s SameSite soubory cookie v ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1ca4f-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="1ca4f-104">Autor: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1ca4f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="1ca4f-105">SameSite je Konceptový standard [IETF](https://ietf.org/about/) navržený tak, aby poskytoval určitou ochranu proti útokům prostřednictvím CSRF (pro falšování požadavků mezi lokalitami).</span><span class="sxs-lookup"><span data-stu-id="1ca4f-105">SameSite is an [IETF](https://ietf.org/about/) draft standard designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="1ca4f-106">Původně koncept v [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)se aktualizoval koncept standardu v [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span><span class="sxs-lookup"><span data-stu-id="1ca4f-106">Originally drafted in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), the draft standard was updated in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span></span> <span data-ttu-id="1ca4f-107">Aktualizovaný Standard není zpětně kompatibilní s předchozím standardem, přičemž následující je největší znatelné rozdíly:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-107">The updated standard is not backward compatible with the previous standard, with the following being the most noticeable differences:</span></span>

* <span data-ttu-id="1ca4f-108">Soubory cookie bez hlavičky SameSite se ve výchozím nastavení považují za `SameSite=Lax`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-108">Cookies without SameSite header are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="1ca4f-109">aby bylo možné používat soubory cookie pro více webů, je třeba použít `SameSite=None`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-109">`SameSite=None` must be used to allow cross-site cookie use.</span></span>
* <span data-ttu-id="1ca4f-110">Soubory cookie, které vyhodnotí `SameSite=None`, musí být také označeny jako `Secure`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-110">Cookies that assert `SameSite=None` must also be marked as `Secure`.</span></span>
* <span data-ttu-id="1ca4f-111">U aplikací, které používají [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) , může docházet k problémům s `sameSite=Lax` nebo `sameSite=Strict` soubory cookie, protože `<iframe>` se považují za scénáře mezi lokalitami.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-111">Applications that use [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) may experience issues with `sameSite=Lax` or `sameSite=Strict` cookies because `<iframe>` is treated as cross-site scenarios.</span></span>
* <span data-ttu-id="1ca4f-112">Hodnota `SameSite=None` není povolena [standardem 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07) a způsobí, že některé implementace považují takové soubory cookie za `SameSite=Strict`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-112">The value `SameSite=None` is not allowed by the [2016 standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) and causes some implementations to treat such cookies as `SameSite=Strict`.</span></span> <span data-ttu-id="1ca4f-113">Viz [Podpora starších prohlížečů](#sob) v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-113">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="1ca4f-114">Nastavení `SameSite=Lax` funguje pro většinu souborů cookie aplikace.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-114">The `SameSite=Lax` setting works for most application cookies.</span></span> <span data-ttu-id="1ca4f-115">Některé formy ověřování, jako je [OpenID Connect](https://openid.net/connect/) (OIDC) a [WS-Federation](https://auth0.com/docs/protocols/ws-fed) , jako výchozí vystavení přesměrování na základě.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-115">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="1ca4f-116">Přesměrování na základě příspěvku spustí ochranu prohlížeče SameSite, takže pro tyto součásti je SameSite zakázaný.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-116">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="1ca4f-117">Většina přihlášení [OAuth](https://oauth.net/) není ovlivněná kvůli rozdílům ve způsobu, jakým jsou požadavky v toku.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-117">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="1ca4f-118">Každá komponenta ASP.NET, která generuje soubory cookie, musí rozhodnout, zda je SameSite vhodná.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-118">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

<span data-ttu-id="1ca4f-119">Informace o problémech s aplikacemi po instalaci aktualizací 2019 .NET SameSite najdete v tématu [známé problémy](#known) .</span><span class="sxs-lookup"><span data-stu-id="1ca4f-119">See [Known Issues](#known) for problems with applications after installing the 2019 .Net SameSite updates.</span></span>

## <a name="using-samesite-in-aspnet-472-and-48"></a><span data-ttu-id="1ca4f-120">Použití SameSite v ASP.NET 4.7.2 a 4,8</span><span class="sxs-lookup"><span data-stu-id="1ca4f-120">Using SameSite in ASP.NET 4.7.2 and 4.8</span></span>

<span data-ttu-id="1ca4f-121">.NET 4.7.2 a 4,8 podporují [koncept standard 2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) pro SameSite od vydání aktualizací v prosinci 2019.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-121">.Net 4.7.2 and 4.8 supports the [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite since the release of updates in December 2019.</span></span> <span data-ttu-id="1ca4f-122">Vývojáři mohou programově řídit hodnotu hlavičky SameSite pomocí [vlastnosti HttpCookie. SameSite](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span><span class="sxs-lookup"><span data-stu-id="1ca4f-122">Developers are able to programmatically control the value of the SameSite header using the [HttpCookie.SameSite property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span></span> <span data-ttu-id="1ca4f-123">Nastavení vlastnosti `SameSite` na `Strict`, `Lax`nebo `None` výsledky v těchto hodnotách, které jsou v síti zapisovány pomocí souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-123">Setting the `SameSite` property to `Strict`, `Lax`, or `None` results in those values being written on the network with the cookie.</span></span> <span data-ttu-id="1ca4f-124">Nastavení rovno `(SameSiteMode)(-1)` znamená, že v síti se souborem cookie by neměl být zahrnutá hlavička SameSite.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-124">Setting it equal to `(SameSiteMode)(-1)` indicates that no SameSite header should be included on the network with the cookie.</span></span> <span data-ttu-id="1ca4f-125">[Vlastnost HttpCookie. Secure](/dotnet/api/system.web.httpcookie.secure)nebo ' vlastnost requireSSL ' v konfiguračních souborech lze použít k označení souboru cookie jako `Secure` nebo ne.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-125">The [HttpCookie.Secure Property](/dotnet/api/system.web.httpcookie.secure), or 'requireSSL' in config files, can be used to mark the cookie as `Secure` or not.</span></span>

<span data-ttu-id="1ca4f-126">Nové instance `HttpCookie` budou ve výchozím nastavení `SameSite=(SameSiteMode)(-1)` a `Secure=false`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-126">New `HttpCookie` instances will default to `SameSite=(SameSiteMode)(-1)` and `Secure=false`.</span></span> <span data-ttu-id="1ca4f-127">Tato výchozí nastavení se dají přepsat v konfigurační sekci `system.web/httpCookies`, kde řetězec `"Unspecified"` je uživatelsky přívětivou syntaxí pro `(SameSiteMode)(-1)`, která je jenom pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-127">These defaults can be overridden in the `system.web/httpCookies` configuration section, where the string `"Unspecified"` is a friendly configuration-only syntax for `(SameSiteMode)(-1)`:</span></span>

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

<span data-ttu-id="1ca4f-128">ASP.Net také pro tyto funkce vydává čtyři konkrétní soubory cookie vlastní: anonymní ověřování, ověřování formulářů, stav relace a Správa rolí.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-128">ASP.Net also issues four specific cookies of its own for these features: Anonymous Authentication, Forms Authentication, Session State, and Role Management.</span></span> <span data-ttu-id="1ca4f-129">Instance těchto souborů cookie, které jsou získány v modulu runtime, mohou být manipulovány pomocí `SameSite` a `Secure` vlastností stejně jako jakékoli jiné instance HttpCookie.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-129">Instances of these cookies obtained in runtime can be manipulated using the `SameSite` and `Secure` properties just like any other HttpCookie instance.</span></span> <span data-ttu-id="1ca4f-130">V důsledku patchworkí SameSite Standard se ale možnosti konfigurace pro tyto čtyři soubory cookie neshodují.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-130">However, due to the patchwork emergence of the SameSite standard, configuration options for these four features cookies is inconsistent.</span></span> <span data-ttu-id="1ca4f-131">Příslušné konfigurační oddíly a atributy s výchozími hodnotami jsou uvedeny níže.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-131">The relevant configuration sections and attributes, with defaults, are shown below.</span></span> <span data-ttu-id="1ca4f-132">Pokud není k dispozici žádný `SameSite` nebo `Secure` v atributu pro funkci, pak se tato funkce přepne na výchozí hodnoty nakonfigurované v části `system.web/httpCookies` popsané výše.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-132">If there is no `SameSite` or `Secure` related attribute for a feature, then the feature will fall back on the defaults configured in the `system.web/httpCookies` section discussed above.</span></span>

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

<span data-ttu-id="1ca4f-133">**Poznámka**: možnost Neurčeno je k dispozici pouze pro `system.web/httpCookies@sameSite` v daném okamžiku.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-133">**Note**: 'Unspecified' is only available to `system.web/httpCookies@sameSite` at the moment.</span></span> <span data-ttu-id="1ca4f-134">Doufáme, že přidáte podobnou syntaxi k dříve zobrazeným atributům cookieSameSite v budoucích aktualizacích.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-134">We hope to add similar syntax to the previously shown cookieSameSite attributes in future updates.</span></span> <span data-ttu-id="1ca4f-135">Nastavení `(SameSiteMode)(-1)` v kódu pořád funguje na instancích těchto souborů cookie. \*</span><span class="sxs-lookup"><span data-stu-id="1ca4f-135">Setting `(SameSiteMode)(-1)` in code still works on instances of these cookies.\*</span></span>

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a><span data-ttu-id="1ca4f-136">Změna cílení aplikací .NET</span><span class="sxs-lookup"><span data-stu-id="1ca4f-136">Retarget .NET apps</span></span>

<span data-ttu-id="1ca4f-137">Pro cílení na .NET 4.7.2 nebo novější:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-137">To target .NET 4.7.2 or later:</span></span>

* <span data-ttu-id="1ca4f-138">Zajistěte, aby soubor *Web. config* obsahoval následující:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-138">Ensure *web.config* contains the following:</span></span>  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  <span data-ttu-id="1ca4f-139">Další podrobnosti najdete v [příručce k migraci rozhraní .NET](/dotnet/framework/migration-guide/) .</span><span class="sxs-lookup"><span data-stu-id="1ca4f-139">The [.NET Migration Guide](/dotnet/framework/migration-guide/) has more details.</span></span>

* <span data-ttu-id="1ca4f-140">Ověřte, jestli jsou balíčky NuGet v projektu cílené na správnou verzi rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-140">Verify NuGet packages in the project are targeted at the correct framework version.</span></span> <span data-ttu-id="1ca4f-141">Správnou verzi rozhraní můžete ověřit kontrolou souboru *Packages. config* , například:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-141">You can verify the correct framework version by examining the *packages.config* file, for example:</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  <span data-ttu-id="1ca4f-142">V předchozím souboru *Packages. config* se `Microsoft.ApplicationInsights` balíčku:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-142">In the preceding *packages.config* file, the `Microsoft.ApplicationInsights` package:</span></span>
    * <span data-ttu-id="1ca4f-143">Je zaměřený na rozhraní .NET 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-143">Is  targeted against .NET 4.5.1.</span></span>
    * <span data-ttu-id="1ca4f-144">Měla by mít atribut `targetFramework` aktualizován tak, aby `net472`, pokud existuje aktualizovaný balíček cílený na váš cílový rámec.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-144">Should have its `targetFramework` attribute updated to `net472` if an updated package targeting your framework target exists.</span></span>

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a><span data-ttu-id="1ca4f-145">Verze rozhraní .NET starší než 4.7.2</span><span class="sxs-lookup"><span data-stu-id="1ca4f-145">.NET versions earlier than 4.7.2</span></span>

<span data-ttu-id="1ca4f-146">Společnost Microsoft nepodporuje verze .NET nižší, než 4.7.2 pro zápis atributu souboru cookie stejné lokality.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-146">Microsoft does not support .NET versions lower that 4.7.2 for writing the same-site cookie attribute.</span></span> <span data-ttu-id="1ca4f-147">Nejsme nenašli spolehlivý způsob, jak:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-147">We have not found a reliable way to:</span></span>

* <span data-ttu-id="1ca4f-148">Ujistěte se, že je správně napsaný atribut na základě verze prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-148">Ensure the attribute is written correctly based on browser version.</span></span>
* <span data-ttu-id="1ca4f-149">Zachycujte a upravujete soubory cookie ověřování a relací ve starších verzích rozhraní.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-149">Intercept and adjust authentication and session cookies on older framework versions.</span></span>

### <a name="december-patch-behavior-changes"></a><span data-ttu-id="1ca4f-150">Prosince změny chování opravy</span><span class="sxs-lookup"><span data-stu-id="1ca4f-150">December patch behavior changes</span></span>

<span data-ttu-id="1ca4f-151">Konkrétní změnou chování pro .NET Framework je způsob, jakým vlastnost `SameSite` interpretuje hodnotu `None`:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-151">The specific behavior change for .NET Framework is how the `SameSite` property interprets the `None` value:</span></span>

* <span data-ttu-id="1ca4f-152">Před opravou hodnoty `None` určena:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-152">Before the patch a value of `None` meant:</span></span>
  * <span data-ttu-id="1ca4f-153">Negenerovat atribut vůbec.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-153">Do not emit the attribute at all.</span></span>
* <span data-ttu-id="1ca4f-154">Po opravě:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-154">After the patch:</span></span>
  * <span data-ttu-id="1ca4f-155">Hodnota `None`znamená "vygenerovat atribut s hodnotou `None`".</span><span class="sxs-lookup"><span data-stu-id="1ca4f-155">A value of `None`it means "Emit the attribute with a value of `None`".</span></span>
  * <span data-ttu-id="1ca4f-156">Hodnota `SameSite` `(SameSiteMode)(-1)` způsobí, že se atribut neemituje.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-156">A `SameSite` value of `(SameSiteMode)(-1)` causes the attribute not to be emitted.</span></span>

<span data-ttu-id="1ca4f-157">Výchozí hodnota SameSite pro ověřování pomocí formulářů a soubory cookie stavu relace se změnila z `None` na `Lax`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-157">The default SameSite value for forms authentication and session state cookies was changed from `None` to `Lax`.</span></span>

### <a name="summary-of-change-impact-on-browsers"></a><span data-ttu-id="1ca4f-158">Shrnutí dopadu na změnu v prohlížečích</span><span class="sxs-lookup"><span data-stu-id="1ca4f-158">Summary of change impact on browsers</span></span>

<span data-ttu-id="1ca4f-159">Pokud nainstalujete opravu a vydáte soubor cookie s `SameSite.None`, dojde k jedné ze dvou akcí:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-159">If you install the patch and issue a cookie with `SameSite.None`, one of two things will happen:</span></span>
* <span data-ttu-id="1ca4f-160">V80 Chrome tento soubor cookie zachová podle nové implementace a neuplatní pro tento soubor cookie stejná omezení webu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-160">Chrome v80 will treat this cookie according to the new implementation, and not enforce same site restrictions on the cookie.</span></span>
* <span data-ttu-id="1ca4f-161">Všechny prohlížeče, které nebyly aktualizovány pro podporu nové implementace, budou následovat po původní implementaci.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-161">Any browser that has not been updated to support the new implementation will follow the old implementation.</span></span> <span data-ttu-id="1ca4f-162">Stará implementace říká:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-162">The old implementation says:</span></span>
  * <span data-ttu-id="1ca4f-163">Pokud se vám zobrazí hodnota, kterou nerozumíte, ignorujte ji a přepněte na přísná omezení lokalit.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-163">If you see a value you don't understand, ignore it and switch to strict same site restrictions.</span></span>

<span data-ttu-id="1ca4f-164">Takže se aplikace buď poruší, nebo dojde k přerušení na mnoha dalších místech.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-164">So either the app breaks in Chrome, or you break in numerous other places.</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="1ca4f-165">Historie a změny</span><span class="sxs-lookup"><span data-stu-id="1ca4f-165">History and changes</span></span>

<span data-ttu-id="1ca4f-166">Podpora SameSite byla poprvé implementována v .NET 4.7.2 s využitím [konceptu standard 2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span><span class="sxs-lookup"><span data-stu-id="1ca4f-166">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="1ca4f-167">19. listopadu 2019 aktualizace pro Windows aktualizované .NET 4.7.2 + od standardu 2016 až do standardu 2019.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-167">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="1ca4f-168">Další aktualizace jsou k disdobu pro jiné verze systému Windows.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-168">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="1ca4f-169">Další informace najdete v tématu <xref:samesite/kbs-samesite>.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-169">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="1ca4f-170">Koncept 2019 specifikace SameSite:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-170">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="1ca4f-171">Není **zpětně** kompatibilní s konceptem 2016.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-171">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="1ca4f-172">Další informace najdete v tématu [Podpora starších prohlížečů](#sob) v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-172">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="1ca4f-173">Určuje, že soubory cookie se ve výchozím nastavení považují za `SameSite=Lax`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-173">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="1ca4f-174">Určuje soubory cookie, které explicitně vyhodnotí `SameSite=None`, aby bylo možné povolit doručování mezi weby, musí být označeno jako `Secure`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-174">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should also be marked as `Secure`.</span></span>
* <span data-ttu-id="1ca4f-175">Je podporován opravami vydanými podle výše uvedených v článku znalostní báze.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-175">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="1ca4f-176">Ve výchozím nastavení je naplánovaná podpora [Chrome](https://chromestatus.com/feature/5088147346030592) v [únoru 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span><span class="sxs-lookup"><span data-stu-id="1ca4f-176">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="1ca4f-177">Prohlížeče začaly při přesunu do tohoto standardu v 2019.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-177">Browsers started moving to this standard in 2019.</span></span>

<a name="known"><a/>

## <a name="known-issues"></a><span data-ttu-id="1ca4f-178">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="1ca4f-178">Known Issues</span></span>

<span data-ttu-id="1ca4f-179">Vzhledem k tomu, že specifikace konceptu 2016 a 2019 nejsou kompatibilní, aktualizace 2019 pro rozhraní .NET Framework zavádí některé změny, které mohou být přerušují.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-179">Because the 2016 and 2019 draft specifications are not compatible, the November 2019 .Net Framework update introduces some changes that may be breaking.</span></span>

* <span data-ttu-id="1ca4f-180">Soubory cookie pro ověření stavu relace a formulářů jsou nyní zapisovány do sítě, protože místo nespecifikovaného je `Lax`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-180">Session State and Forms Authentication cookies are now written to the network as `Lax` instead of unspecified.</span></span>
  * <span data-ttu-id="1ca4f-181">I když většina aplikací spolupracuje s `SameSite=Lax` soubory cookie, aplikace, které odesílají weby nebo aplikace, které využívají `iframe`, můžou zjistit, že se jejich stav relace nebo soubory cookie autorizace formulářů nepoužívají podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-181">While most apps work with `SameSite=Lax` cookies, apps that POST across sites or applications that make use of `iframe` may find that their session state or forms authorization cookies aren't being used as expected.</span></span> <span data-ttu-id="1ca4f-182">Pokud to chcete napravit, změňte hodnotu `cookieSameSite` v příslušném konfiguračním oddílu, jak je popsáno výše.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-182">To remedy this, change the `cookieSameSite` value in the appropriate configuration section as discussed previously.</span></span>
* <span data-ttu-id="1ca4f-183">HttpCookies, který explicitně nastaví `SameSite=None` v kódu nebo v konfiguraci, má nyní tuto hodnotu napsanou v souboru cookie, zatímco dříve byla vynechána.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-183">HttpCookies that explicitly set `SameSite=None` in code or configuration now have that value written with the cookie, whereas it was previously omitted.</span></span> <span data-ttu-id="1ca4f-184">To může způsobit problémy se staršími prohlížeči, které podporují jenom 2016 koncept Standard.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-184">This may cause issues with older browsers that only support the 2016 draft standard.</span></span>
  * <span data-ttu-id="1ca4f-185">Když cílíte na prohlížeče, které podporují pracovní Standard 2019 s `SameSite=None` soubory cookie, nezapomeňte je také označit `Secure` nebo nemusejí být rozpoznány.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-185">When targeting browsers supporting the 2019 draft standard with `SameSite=None` cookies, remember to also mark them `Secure` or they may not be recognized.</span></span>
  * <span data-ttu-id="1ca4f-186">Pokud se chcete vrátit k 2016 chování, které nepíše `SameSite=None`, použijte nastavení aplikace `aspnet:SupressSameSiteNone=true`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-186">To revert to the 2016 behavior of not writing `SameSite=None`, use the app setting `aspnet:SupressSameSiteNone=true`.</span></span> <span data-ttu-id="1ca4f-187">Všimněte si, že tato akce bude platit pro všechny HttpCookies v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-187">Note that this will apply to all HttpCookies in the app.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="1ca4f-188">Azure App Service – zpracování souborů cookie SameSite</span><span class="sxs-lookup"><span data-stu-id="1ca4f-188">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="1ca4f-189">Informace o tom, jak Azure App Service konfiguruje chování SameSite v aplikacích .NET 4.7.2, najdete v tématu [Azure App Service – zpracování souborů cookie SameSite a .NET Framework opravy 4.7.2](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) .</span><span class="sxs-lookup"><span data-stu-id="1ca4f-189">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for information about how Azure App Service is configuring SameSite behaviors in .Net 4.7.2 apps.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="1ca4f-190">Podpora starších prohlížečů</span><span class="sxs-lookup"><span data-stu-id="1ca4f-190">Supporting older browsers</span></span>

<span data-ttu-id="1ca4f-191">SameSite standardně vyhodnocuje, že neznámé hodnoty musí být považovány za `SameSite=Strict` hodnoty. 2016</span><span class="sxs-lookup"><span data-stu-id="1ca4f-191">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="1ca4f-192">Aplikace, ke kterým se přistupoval ze starších prohlížečů, které podporují SameSite úrovně Standard 2016, se můžou přerušit, když získají vlastnost SameSite s hodnotou `None`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-192">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="1ca4f-193">Webové aplikace musí implementovat detekci prohlížeče, pokud chtějí podporovat starší prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-193">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="1ca4f-194">ASP.NET neimplementuje zjišťování prohlížeče, protože hodnoty uživatelských agentů jsou vysoce těkavé a často se mění.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-194">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span>

<span data-ttu-id="1ca4f-195">Přístup společnosti Microsoft k řešení problému vám usnadní implementaci komponent detekce prohlížeče, aby bylo možné z souborů cookie nakládat atribut `sameSite=None`, pokud je známo, že ho prohlížeč nepodporují.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-195">Microsoft's approach to fixing the problem is to help you implement browser detection components to strip the `sameSite=None` attribute from cookies if a browser is known to not support it.</span></span> <span data-ttu-id="1ca4f-196">Při poradenství od společnosti Google bylo nutné vystavit dvojité soubory cookie, jeden s novým atributem a druhý bez atributu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-196">Google's advice was to issue double cookies, one with the new attribute, and one without the attribute at all.</span></span> <span data-ttu-id="1ca4f-197">Doporučujeme však, abyste považovat jenom na Rady Google.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-197">However we consider Google's advice limited.</span></span> <span data-ttu-id="1ca4f-198">Některé prohlížeče, zejména mobilní prohlížeče, mají velmi malá omezení počtu souborů cookie, které web nebo název domény může odeslat.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-198">Some browsers, especially mobile browsers have very small limits on the number of cookies a site, or a domain name can send.</span></span> <span data-ttu-id="1ca4f-199">Odesílání více souborů cookie, zejména velkých souborů cookie, jako jsou soubory cookie pro ověřování, může dosáhnout vysokého limitu, což způsobí selhání aplikací, které je obtížné diagnostikovat a opravovat.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-199">Sending multiple cookies, especially large cookies like authentication cookies can reach the mobile browser limit very quickly, causing app failures that are hard to diagnose and fix.</span></span> <span data-ttu-id="1ca4f-200">Kromě architektury existuje velký ekosystém kódu a komponent třetích stran, které nemusejí být aktualizovány, aby používaly přístup pomocí dvojitých souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-200">Furthermore as a framework there is a large ecosystem of third party code and components that may not be updated to use a double cookie approach.</span></span>

<span data-ttu-id="1ca4f-201">Kód pro detekci prohlížeče použitý v ukázkových projektech v [tomto úložišti GitHubu]() je obsažen ve dvou souborech.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-201">The browser detection code used in the sample projects in [this GitHub repository]() is contained in two files</span></span>

* [<span data-ttu-id="1ca4f-202">C#SameSiteSupport.cs</span><span class="sxs-lookup"><span data-stu-id="1ca4f-202">C# SameSiteSupport.cs</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [<span data-ttu-id="1ca4f-203">VB SameSiteSupport. vb</span><span class="sxs-lookup"><span data-stu-id="1ca4f-203">VB SameSiteSupport.vb</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

<span data-ttu-id="1ca4f-204">Tyto detekce jsou nejběžnějšími agenty prohlížeče, kteří viděli, že podporují Standard 2016 a pro které je potřeba atribut úplně odebrat.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-204">These detections are the most common browser agents we have seen that support the 2016 standard and for which the attribute needs to be completely removed.</span></span> <span data-ttu-id="1ca4f-205">Není určena jako kompletní implementace:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-205">It isn't meant as a complete implementation:</span></span>

* <span data-ttu-id="1ca4f-206">Vaše aplikace může zobrazit prohlížeče, které naše testovací weby nepodporují.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-206">Your app may see browsers that our test sites do not.</span></span>
* <span data-ttu-id="1ca4f-207">Měli byste být připraveni přidat detekce podle potřeby vašeho prostředí.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-207">You should be prepared to add detections as necessary for your environment.</span></span>

<span data-ttu-id="1ca4f-208">Způsob, jakým se detekuje detekce, se liší podle verze rozhraní .NET a webového rozhraní, které používáte.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-208">How you wire up the detection varies according the version of .NET and the web framework that you are using.</span></span> <span data-ttu-id="1ca4f-209">Následující kód lze volat na webu <xref:HTTP.HttpCookie> volání:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-209">The following code can be called at the <xref:HTTP.HttpCookie> call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="1ca4f-210">Podívejte se na následující témata ASP.NET souborů cookie 4.7.2 SameSite:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-210">See the following ASP.NET 4.7.2 SameSite cookie topics:</span></span>

* [<span data-ttu-id="1ca4f-211">C#NÁVRHOVÝ</span><span class="sxs-lookup"><span data-stu-id="1ca4f-211">C# MVC</span></span>](xref:samesite/csMVC)
* [<span data-ttu-id="1ca4f-212">C#Webových formulářů</span><span class="sxs-lookup"><span data-stu-id="1ca4f-212">C# WebForms</span></span>](xref:samesite/CSharpWebForms)
* [<span data-ttu-id="1ca4f-213">Webforma VB</span><span class="sxs-lookup"><span data-stu-id="1ca4f-213">VB WebForms</span></span>](xref:samesite/vbWF)
* [<span data-ttu-id="1ca4f-214">VB MVC</span><span class="sxs-lookup"><span data-stu-id="1ca4f-214">VB MVC</span></span>](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a><span data-ttu-id="1ca4f-215">Zajištění přesměrování lokality na HTTPS</span><span class="sxs-lookup"><span data-stu-id="1ca4f-215">Ensuring your site redirects to HTTPS</span></span>

<span data-ttu-id="1ca4f-216">Pro přesměrování všech požadavků na protokol HTTPS se dá použít funkce pro [přepsání adresy URL služby](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) ASP.NET 4. x, WebForms a MVC.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-216">For ASP.NET 4.x, WebForms and MVC, [IIS's URL Rewrite](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) feature can be used to redirect all requests to HTTPS.</span></span> <span data-ttu-id="1ca4f-217">Následující kód XML ukazuje vzorové pravidlo:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-217">The following XML shows a sample rule:</span></span>

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

<span data-ttu-id="1ca4f-218">V místních instalacích opětovného [zápisu adres URL IIS](https://www.iis.net/downloads/microsoft/url-rewrite) je volitelná funkce, která může být potřeba nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-218">In on-premises installations of [IIS URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) is an optional feature that may need installing.</span></span>

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="1ca4f-219">Testování aplikací pro problémy s SameSite</span><span class="sxs-lookup"><span data-stu-id="1ca4f-219">Test apps for SameSite problems</span></span>

<span data-ttu-id="1ca4f-220">Aplikaci musíte otestovat pomocí prohlížečů, které podporujete, a Projděte si scénáře, které zahrnují soubory cookie.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-220">You must test your app with the browsers you support and go through your scenarios that involve cookies.</span></span> <span data-ttu-id="1ca4f-221">Scénáře souborů cookie obvykle zahrnují</span><span class="sxs-lookup"><span data-stu-id="1ca4f-221">Cookie scenarios typically involve</span></span>

* <span data-ttu-id="1ca4f-222">Formuláře pro přihlášení</span><span class="sxs-lookup"><span data-stu-id="1ca4f-222">Login forms</span></span>
* <span data-ttu-id="1ca4f-223">Externí mechanismy přihlášení, jako je Facebook, Azure AD, OAuth a OIDC</span><span class="sxs-lookup"><span data-stu-id="1ca4f-223">External login mechanisms such as Facebook, Azure AD, OAuth and OIDC</span></span>
* <span data-ttu-id="1ca4f-224">Stránky, které přijímají žádosti z jiných lokalit</span><span class="sxs-lookup"><span data-stu-id="1ca4f-224">Pages that accept requests from other sites</span></span>
* <span data-ttu-id="1ca4f-225">Stránky v aplikaci navržené tak, aby byly vložené v iFrames</span><span class="sxs-lookup"><span data-stu-id="1ca4f-225">Pages in your app designed to be embedded in iframes</span></span>

<span data-ttu-id="1ca4f-226">Měli byste kontrolovat, jestli jsou soubory cookie vytvořené, trvalé a odstraněné ve vaší aplikaci správně.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-226">You should check that cookies are created, persisted and deleted correctly in your app.</span></span>

<span data-ttu-id="1ca4f-227">Aplikace, které komunikují se vzdálenými lokalitami, jako je třeba přihlášení třetí strany, potřebují:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-227">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="1ca4f-228">Otestujte interakci na více prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-228">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="1ca4f-229">Použití [zjišťování a zmírnění](#sob) problémů v prohlížeči, které jsou popsány v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-229">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="1ca4f-230">Otestujte webové aplikace pomocí verze klienta, která se může přihlásit k novému chování SameSite.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-230">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="1ca4f-231">Pro Chrome, Firefox a chrom Edge mají všechny nové příznaky funkcí pro výslovný souhlas, které lze použít k testování.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-231">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="1ca4f-232">Po použití oprav SameSite se aplikace testuje se staršími verzemi klientů, zejména Safari.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-232">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="1ca4f-233">Další informace najdete v tématu [Podpora starších prohlížečů](#sob) v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-233">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="1ca4f-234">Testování s použitím Chromu</span><span class="sxs-lookup"><span data-stu-id="1ca4f-234">Test with Chrome</span></span>

<span data-ttu-id="1ca4f-235">Chrome 78 + poskytuje zavádějící výsledky, protože má na zpracování dočasné omezení.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-235">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="1ca4f-236">Chrome 78 + dočasné zmírnění umožňuje, aby soubory cookie byly starší než dvě minuty.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-236">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="1ca4f-237">Chrome 76 nebo 77 s povolenými vhodnými příznakem testu poskytuje přesnější výsledky.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-237">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="1ca4f-238">Chcete-li otestovat nové chování SameSite, přepněte `chrome://flags/#same-site-by-default-cookies` na **povoleno**.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-238">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="1ca4f-239">Starší verze Chrome (75 a novější) jsou hlášeny jako neúspěšné s novým nastavením `None`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-239">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="1ca4f-240">Viz [Podpora starších prohlížečů](#sob) v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-240">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="1ca4f-241">Google nezpřístupňuje starší verze Chrome.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-241">Google does not make older chrome versions available.</span></span> <span data-ttu-id="1ca4f-242">Postupujte podle pokynů v části [stažení Chromu](https://www.chromium.org/getting-involved/download-chromium) a otestujte starší verze Chrome.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-242">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="1ca4f-243">Nestahujte Chrome z odkazů **, které jsou** k dispozici, hledáním ve starších verzích Chrome.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-243">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="1ca4f-244">Chróm 76 Win64</span><span class="sxs-lookup"><span data-stu-id="1ca4f-244">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="1ca4f-245">Chróm 74 Win64</span><span class="sxs-lookup"><span data-stu-id="1ca4f-245">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* <span data-ttu-id="1ca4f-246">Pokud nepoužíváte 64bitovou verzi systému Windows, můžete pomocí [prohlížeče OmahaProxy](https://omahaproxy.appspot.com/) vyhledat, která větev Chromu odpovídá stylu Chrome 74 (v 74.0.3729.108), a to podle [pokynů uvedených v Chromu](https://www.chromium.org/getting-involved/download-chromium).</span><span class="sxs-lookup"><span data-stu-id="1ca4f-246">If you're not using a 64bit version of Windows you can use the [OmahaProxy viewer](https://omahaproxy.appspot.com/) to look up which Chromium branch corresponds to Chrome 74 (v74.0.3729.108) using the [instructions provided by Chromium](https://www.chromium.org/getting-involved/download-chromium).</span></span>

#### <a name="test-with-chrome-80"></a><span data-ttu-id="1ca4f-247">Testování s použitím Chromu 80 +</span><span class="sxs-lookup"><span data-stu-id="1ca4f-247">Test with Chrome 80+</span></span>

<span data-ttu-id="1ca4f-248">[Stáhněte si](https://www.google.com/chrome/) verzi Chrome, která podporuje jejich nový atribut.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-248">[Download](https://www.google.com/chrome/) a version of Chrome that supports their new attribute.</span></span> <span data-ttu-id="1ca4f-249">V době psaní je aktuální verze Chrome 80.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-249">At the time of writing, the current version is Chrome 80.</span></span> <span data-ttu-id="1ca4f-250">Chrome 80 vyžaduje, aby byl příznak `chrome://flags/#same-site-by-default-cookies` povolen pro použití nového chování.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-250">Chrome 80 needs the flag `chrome://flags/#same-site-by-default-cookies` enabled to use the new behavior.</span></span> <span data-ttu-id="1ca4f-251">Měli byste taky povolit (`chrome://flags/#cookies-without-same-site-must-be-secure`) pro otestování nadcházejícího chování souborů cookie, u kterých není povolený žádný atribut sameSite.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-251">You should also enable (`chrome://flags/#cookies-without-same-site-must-be-secure`) to test the upcoming behavior for cookies which have no sameSite attribute enabled.</span></span> <span data-ttu-id="1ca4f-252">Chrome 80 je v cíli, aby tento přepínač považoval soubory cookie bez atributu `SameSite=Lax`, i když s časovým obdobím pro určité žádosti.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-252">Chrome 80 is on target to make the switch to treat cookies without the attribute as `SameSite=Lax`, albeit with a timed grace period for certain requests.</span></span> <span data-ttu-id="1ca4f-253">Chcete-li zakázat časový limit doby odkladu, je možné spustit Chrome 80 s následujícím argumentem příkazového řádku:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-253">To disable the timed grace period Chrome 80 can be launched with the following command line argument:</span></span>

`--enable-features=SameSiteDefaultChecksMethodRigorously`

<span data-ttu-id="1ca4f-254">Chrome 80 obsahuje varovné zprávy v konzole prohlížeče o chybějících atributech sameSite.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-254">Chrome 80 has warning messages in the browser console about missing sameSite attributes.</span></span> <span data-ttu-id="1ca4f-255">Pomocí F12 otevřete konzolu prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-255">Use F12 to open the browser console.</span></span>

### <a name="test-with-safari"></a><span data-ttu-id="1ca4f-256">Testování pomocí Safari</span><span class="sxs-lookup"><span data-stu-id="1ca4f-256">Test with Safari</span></span>

<span data-ttu-id="1ca4f-257">Prohlížeč Safari 12 striktně implementuje předchozí koncept a v případě, že je nová hodnota `None` v souboru cookie, se nezdařila.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-257">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="1ca4f-258">`None` se vyhnete prostřednictvím kódu detekce prohlížeče, který [podporuje starší prohlížeče](#sob) v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-258">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="1ca4f-259">Pomocí MSAL, ADAL nebo libovolné knihovny, kterou používáte, otestujte přihlašovací údaje pro WebKit Safari 12, Safari 13 a na bázi.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-259">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="1ca4f-260">Problém závisí na základní verzi operačního systému.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-260">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="1ca4f-261">OSX Mojave (10,14) a iOS 12 se nazývají problémy s kompatibilitou s novým chováním SameSite.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-261">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="1ca4f-262">Upgrade operačního systému na OSX Catalina (10,15) nebo iOS 13 opravuje problém.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-262">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="1ca4f-263">Prohlížeč Safari aktuálně nemá příznak výslovných přihlášení pro testování nového chování specifikace.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-263">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="1ca4f-264">Testování pomocí Firefox</span><span class="sxs-lookup"><span data-stu-id="1ca4f-264">Test with Firefox</span></span>

<span data-ttu-id="1ca4f-265">Podporu aplikace Firefox pro nový standard lze testovat na verzi 68 + tím, že na stránce `about:config` `network.cookie.sameSite.laxByDefault`příznak funkce.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-265">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="1ca4f-266">Nebyly zjištěny žádné zprávy o problémech s kompatibilitou se staršími verzemi aplikace Firefox.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-266">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-legacy-browser"></a><span data-ttu-id="1ca4f-267">Test pomocí prohlížeče Edge (starší verze)</span><span class="sxs-lookup"><span data-stu-id="1ca4f-267">Test with Edge (Legacy) browser</span></span>

<span data-ttu-id="1ca4f-268">Edge podporuje starý SameSite Standard.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-268">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="1ca4f-269">Edge verze 44 + nemá žádné známé problémy s kompatibilitou s novým standardem.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-269">Edge version 44+ doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="1ca4f-270">Test s hranou (chrom)</span><span class="sxs-lookup"><span data-stu-id="1ca4f-270">Test with Edge (Chromium)</span></span>

<span data-ttu-id="1ca4f-271">Příznaky SameSite jsou nastaveny na stránce `edge://flags/#same-site-by-default-cookies`.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-271">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="1ca4f-272">U Edge Chromu se nezjistily žádné problémy s kompatibilitou.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-272">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="1ca4f-273">Testování s elektronem</span><span class="sxs-lookup"><span data-stu-id="1ca4f-273">Test with Electron</span></span>

<span data-ttu-id="1ca4f-274">K verzím elektronů patří starší verze Chromu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-274">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="1ca4f-275">Například verze elektronicky používané týmy je chrom 66, který vykazuje starší chování.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-275">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="1ca4f-276">Je nutné provést vlastní testování kompatibility s verzí elektronů, kterou váš produkt používá.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-276">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="1ca4f-277">Viz [Podpora starších prohlížečů](#sob).</span><span class="sxs-lookup"><span data-stu-id="1ca4f-277">See [Supporting older browsers](#sob).</span></span>

## <a name="reverting-samesite-patches"></a><span data-ttu-id="1ca4f-278">Vracení SameSite oprav</span><span class="sxs-lookup"><span data-stu-id="1ca4f-278">Reverting SameSite patches</span></span>

<span data-ttu-id="1ca4f-279">Můžete obnovit aktualizované chování sameSite v aplikaci .NET Framework aplikace na předchozí chování, kde atribut sameSite není generován pro hodnotu `None`a vrátit soubory cookie ověřování a relace, aby negenerovaly hodnotu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-279">You can revert the updated sameSite behavior in .NET Framework apps to its previous behavior where the sameSite attribute is not emitted for a value of `None`, and revert the authentication and session cookies to not emit the value.</span></span> <span data-ttu-id="1ca4f-280">Tato akce by se měla zobrazit jako *extrémně dočasná oprava*, protože změny v Chromu přeruší všechny požadavky externích příspěvků nebo ověřování pro uživatele pomocí prohlížečů, které podporují změny standardu.</span><span class="sxs-lookup"><span data-stu-id="1ca4f-280">This should be viewed as an *extremely temporary fix*, as the Chrome changes will break any external POST requests or authentication for users using browsers which support the changes to the standard.</span></span>

### <a name="reverting-net-472-behavior"></a><span data-ttu-id="1ca4f-281">Vrácení chování .NET 4.7.2</span><span class="sxs-lookup"><span data-stu-id="1ca4f-281">Reverting .NET 4.7.2 behavior</span></span>

<span data-ttu-id="1ca4f-282">Aktualizujte soubor *Web. config* tak, aby zahrnoval následující nastavení konfigurace:</span><span class="sxs-lookup"><span data-stu-id="1ca4f-282">Update *web.config* to include the following configuration settings:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="1ca4f-283">Další materiály a zdroje informací</span><span class="sxs-lookup"><span data-stu-id="1ca4f-283">Additional resources</span></span>

* [<span data-ttu-id="1ca4f-284">Nadcházející změny souborů cookie SameSite v ASP.NET a ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1ca4f-284">Upcoming SameSite Cookie Changes in ASP.NET and ASP.NET Core</span></span>](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [<span data-ttu-id="1ca4f-285">Chromový blog: vývojáři: Připravte se na nové SameSite = None; Nastavení zabezpečeného souboru cookie</span><span class="sxs-lookup"><span data-stu-id="1ca4f-285">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="1ca4f-286">Vysvětlení souborů cookie SameSite</span><span class="sxs-lookup"><span data-stu-id="1ca4f-286">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="1ca4f-287">Aktualizace pro Chrome</span><span class="sxs-lookup"><span data-stu-id="1ca4f-287">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)
* [<span data-ttu-id="1ca4f-288">Opravy .NET SameSite</span><span class="sxs-lookup"><span data-stu-id="1ca4f-288">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)
* [<span data-ttu-id="1ca4f-289">Informace o stejných lokalitách webových aplikací Azure</span><span class="sxs-lookup"><span data-stu-id="1ca4f-289">Azure Web Applications Same Site Information</span></span>](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [<span data-ttu-id="1ca4f-290">Informace o stejných lokalitách Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ca4f-290">Azure ActiveDirectory Same Site Information</span></span>](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)

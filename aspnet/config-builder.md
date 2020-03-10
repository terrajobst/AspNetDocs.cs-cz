---
uid: config-builder
title: Tvůrci konfigurace pro ASP.NET
author: rick-anderson
description: Naučte se získat konfigurační data z jiných zdrojů než hodnot Web. config z externích zdrojů.
ms.author: riande
ms.date: 10/29/2018
msc.type: content
ms.openlocfilehash: 5299d9ab057c3096773955a7461e77a80673ebfe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584509"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="421b1-103">Tvůrci konfigurace pro ASP.NET</span><span class="sxs-lookup"><span data-stu-id="421b1-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="421b1-104">Od [Stephen Molloy](https://github.com/StephenMolloy) a [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="421b1-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="421b1-105">Tvůrci konfigurace poskytují moderní a agilní mechanizmus pro aplikace ASP.NET k získání hodnot konfigurace z externích zdrojů.</span><span class="sxs-lookup"><span data-stu-id="421b1-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="421b1-106">Tvůrci konfigurace:</span><span class="sxs-lookup"><span data-stu-id="421b1-106">Configuration builders:</span></span>

* <span data-ttu-id="421b1-107">Jsou k dispozici v .NET Framework 4.7.1 a novějším.</span><span class="sxs-lookup"><span data-stu-id="421b1-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="421b1-108">Poskytněte flexibilní mechanizmus pro čtení hodnot konfigurace.</span><span class="sxs-lookup"><span data-stu-id="421b1-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="421b1-109">Při přesunu do kontejneru a prostředí zaměřeného na Cloud se řeší některé základní požadavky aplikací.</span><span class="sxs-lookup"><span data-stu-id="421b1-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="421b1-110">Dá se použít ke zlepšení ochrany konfiguračních dat vykreslováním ze zdrojů, které byly dřív nedostupné (například Azure Key Vault a proměnných prostředí) v konfiguračním systému .NET.</span><span class="sxs-lookup"><span data-stu-id="421b1-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="421b1-111">Tvůrci konfigurace klíč/hodnota</span><span class="sxs-lookup"><span data-stu-id="421b1-111">Key/value configuration builders</span></span>

<span data-ttu-id="421b1-112">Běžným scénářem, který mohou být zpracovány konfiguračními sestavami, je poskytnout základní mechanismus pro nahrazení klíč/hodnota pro konfigurační oddíly, které následují po vzorci klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="421b1-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="421b1-113">.NET Framework koncept ConfigurationBuilders není omezený na konkrétní konfigurační oddíly nebo vzory.</span><span class="sxs-lookup"><span data-stu-id="421b1-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="421b1-114">Mnoho konfiguračních sestavení v `Microsoft.Configuration.ConfigurationBuilders` ([GitHub](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) ale funguje v rámci vzoru klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="421b1-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="421b1-115">Nastavení tvůrců konfigurace klíč/hodnota</span><span class="sxs-lookup"><span data-stu-id="421b1-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="421b1-116">Následující nastavení platí pro všechna sestavení konfigurace klíč/hodnota v `Microsoft.Configuration.ConfigurationBuilders`.</span><span class="sxs-lookup"><span data-stu-id="421b1-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="421b1-117">Režim</span><span class="sxs-lookup"><span data-stu-id="421b1-117">Mode</span></span>

<span data-ttu-id="421b1-118">Tvůrci konfigurace používají externí zdroj informací o klíčích a hodnotách k naplnění vybraných prvků klíč/hodnota konfiguračního systému.</span><span class="sxs-lookup"><span data-stu-id="421b1-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="421b1-119">Konkrétně oddíly `<appSettings/>` a `<connectionStrings/>` dostanou zvláštní zacházení od tvůrců konfigurace.</span><span class="sxs-lookup"><span data-stu-id="421b1-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="421b1-120">Tvůrci pracují ve třech režimech:</span><span class="sxs-lookup"><span data-stu-id="421b1-120">The builders work in three modes:</span></span>

* <span data-ttu-id="421b1-121">`Strict` – výchozí režim.</span><span class="sxs-lookup"><span data-stu-id="421b1-121">`Strict` - The default mode.</span></span> <span data-ttu-id="421b1-122">V tomto režimu nástroj Configuration Builder pracuje pouze s dobře známými konfiguračními oddíly orientovanými na klíč/hodnotu.</span><span class="sxs-lookup"><span data-stu-id="421b1-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="421b1-123">`Strict` režim vytvoří výčet jednotlivých klíčů v části.</span><span class="sxs-lookup"><span data-stu-id="421b1-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="421b1-124">Pokud je v externím zdroji nalezen shodný klíč:</span><span class="sxs-lookup"><span data-stu-id="421b1-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="421b1-125">Tvůrci konfigurace nahradí hodnotu ve výsledném oddílu konfigurace hodnotou z externího zdroje.</span><span class="sxs-lookup"><span data-stu-id="421b1-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="421b1-126">`Greedy` – tento režim úzce souvisí s režimem `Strict`.</span><span class="sxs-lookup"><span data-stu-id="421b1-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="421b1-127">Místo toho, aby se omezily na klíče, které už existují v původní konfiguraci:</span><span class="sxs-lookup"><span data-stu-id="421b1-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="421b1-128">Tvůrci konfigurace přidají všechny páry klíč/hodnota z externího zdroje do výsledného konfiguračního oddílu.</span><span class="sxs-lookup"><span data-stu-id="421b1-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="421b1-129">`Expand` – funguje v nezpracovaném formátu XML před tím, než se analyzuje do objektu konfiguračního oddílu.</span><span class="sxs-lookup"><span data-stu-id="421b1-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="421b1-130">Lze si představit jako rozšíření tokenů v řetězci.</span><span class="sxs-lookup"><span data-stu-id="421b1-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="421b1-131">Jakákoli část nezpracovaného řetězce XML, který odpovídá vzoru `${token}`, je kandidátem pro rozšíření tokenu.</span><span class="sxs-lookup"><span data-stu-id="421b1-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="421b1-132">Pokud se v externím zdroji nenajde žádná odpovídající hodnota, token se nemění.</span><span class="sxs-lookup"><span data-stu-id="421b1-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="421b1-133">Tvůrci v tomto režimu nejsou omezeni na oddíly `<appSettings/>` a `<connectionStrings/>`.</span><span class="sxs-lookup"><span data-stu-id="421b1-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="421b1-134">Následující kód ze *souboru Web. config* povolí [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) v režimu `Strict`:</span><span class="sxs-lookup"><span data-stu-id="421b1-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="421b1-135">Následující kód přečte `<appSettings/>` a `<connectionStrings/>` uvedeny v předchozím souboru *Web. config* :</span><span class="sxs-lookup"><span data-stu-id="421b1-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="421b1-136">Předchozí kód nastaví hodnoty vlastností na:</span><span class="sxs-lookup"><span data-stu-id="421b1-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="421b1-137">Hodnoty v souboru *Web. config* , pokud klíče nejsou nastaveny v proměnných prostředí.</span><span class="sxs-lookup"><span data-stu-id="421b1-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="421b1-138">Hodnoty proměnné prostředí, je-li nastavena.</span><span class="sxs-lookup"><span data-stu-id="421b1-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="421b1-139">`ServiceID` například bude obsahovat:</span><span class="sxs-lookup"><span data-stu-id="421b1-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="421b1-140">"Idslužby hodnota z Web. config", pokud není nastavená proměnná prostředí `ServiceID`.</span><span class="sxs-lookup"><span data-stu-id="421b1-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="421b1-141">Hodnota proměnné prostředí `ServiceID`, je-li nastavena.</span><span class="sxs-lookup"><span data-stu-id="421b1-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="421b1-142">Následující obrázek ukazuje `<appSettings/>` klíče nebo hodnoty z předchozího souboru *Web. config* , který je nastaven v editoru prostředí:</span><span class="sxs-lookup"><span data-stu-id="421b1-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![Editor prostředí](config-builder/static/env.png)

<span data-ttu-id="421b1-144">Poznámka: Pokud chcete zobrazit změny v proměnných prostředí, možná budete muset aplikaci Visual Studio ukončit a restartovat.</span><span class="sxs-lookup"><span data-stu-id="421b1-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="421b1-145">Zpracování předpon</span><span class="sxs-lookup"><span data-stu-id="421b1-145">Prefix handling</span></span>

<span data-ttu-id="421b1-146">Klíčové předpony můžou zjednodušit nastavení klíčů z těchto důvodů:</span><span class="sxs-lookup"><span data-stu-id="421b1-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="421b1-147">Konfigurace .NET Framework je složitá a vnořená.</span><span class="sxs-lookup"><span data-stu-id="421b1-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="421b1-148">Zdroje externích klíčů a hodnot jsou běžně základní a ploché podle povahy.</span><span class="sxs-lookup"><span data-stu-id="421b1-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="421b1-149">Například proměnné prostředí nejsou vnořené.</span><span class="sxs-lookup"><span data-stu-id="421b1-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="421b1-150">K vložení `<appSettings/>` a `<connectionStrings/>` do konfigurace prostřednictvím proměnných prostředí použijte některý z následujících přístupů:</span><span class="sxs-lookup"><span data-stu-id="421b1-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="421b1-151">S `EnvironmentConfigBuilder` ve výchozím režimu `Strict` a příslušnými názvy klíčů v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="421b1-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="421b1-152">Předchozí kód a kód přebírají tento přístup.</span><span class="sxs-lookup"><span data-stu-id="421b1-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="421b1-153">Pomocí tohoto přístupu **nemůžete** mít v `<appSettings/>` i `<connectionStrings/>`stejné pojmenované klíče.</span><span class="sxs-lookup"><span data-stu-id="421b1-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="421b1-154">Použijte dva `EnvironmentConfigBuilder`s v režimu `Greedy` s jedinečnými předponami a `stripPrefix`.</span><span class="sxs-lookup"><span data-stu-id="421b1-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="421b1-155">S tímto přístupem může aplikace číst `<appSettings/>` a `<connectionStrings/>` bez nutnosti aktualizovat konfigurační soubor.</span><span class="sxs-lookup"><span data-stu-id="421b1-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="421b1-156">V další části [stripPrefix](#stripprefix)se dozvíte, jak to provést.</span><span class="sxs-lookup"><span data-stu-id="421b1-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="421b1-157">Použijte dva `EnvironmentConfigBuilder`s v režimu `Greedy` s jedinečnými předponami.</span><span class="sxs-lookup"><span data-stu-id="421b1-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="421b1-158">U tohoto přístupu nemůžete mít duplicitní názvy klíčů, protože názvy klíčů se musí lišit podle předpony.</span><span class="sxs-lookup"><span data-stu-id="421b1-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="421b1-159">Příklad:</span><span class="sxs-lookup"><span data-stu-id="421b1-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="421b1-160">S předchozím označením je možné použít stejný zdroj nestrukturovaného klíče nebo hodnoty k naplnění konfigurace dvou různých oddílů.</span><span class="sxs-lookup"><span data-stu-id="421b1-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="421b1-161">Následující obrázek ukazuje `<appSettings/>` a `<connectionStrings/>` klíče/hodnoty z předchozího souboru *Web. config* , který je nastaven v editoru prostředí:</span><span class="sxs-lookup"><span data-stu-id="421b1-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![Editor prostředí](config-builder/static/prefix.png)

<span data-ttu-id="421b1-163">Následující kód přečte `<appSettings/>` a `<connectionStrings/>` klíče/hodnoty obsažené v předchozím souboru *Web. config* :</span><span class="sxs-lookup"><span data-stu-id="421b1-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="421b1-164">Předchozí kód nastaví hodnoty vlastností na:</span><span class="sxs-lookup"><span data-stu-id="421b1-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="421b1-165">Hodnoty v souboru *Web. config* , pokud klíče nejsou nastaveny v proměnných prostředí.</span><span class="sxs-lookup"><span data-stu-id="421b1-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="421b1-166">Hodnoty proměnné prostředí, je-li nastavena.</span><span class="sxs-lookup"><span data-stu-id="421b1-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="421b1-167">Například pomocí předchozího souboru *Web. config* , klíčů/hodnot v předchozí imagi editoru prostředí a předchozího kódu jsou nastaveny následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="421b1-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="421b1-168">Klíč</span><span class="sxs-lookup"><span data-stu-id="421b1-168">Key</span></span>              | <span data-ttu-id="421b1-169">Hodnota</span><span class="sxs-lookup"><span data-stu-id="421b1-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="421b1-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="421b1-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="421b1-171">AppSetting_ServiceID z proměnných ENV</span><span class="sxs-lookup"><span data-stu-id="421b1-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="421b1-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="421b1-172">AppSetting_default</span></span>            | <span data-ttu-id="421b1-173">AppSetting_default hodnota z ENV</span><span class="sxs-lookup"><span data-stu-id="421b1-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="421b1-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="421b1-174">ConnStr_default</span></span>         | <span data-ttu-id="421b1-175">ConnStr_default Val ze ENV</span><span class="sxs-lookup"><span data-stu-id="421b1-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="421b1-176">stripPrefix</span><span class="sxs-lookup"><span data-stu-id="421b1-176">stripPrefix</span></span>

<span data-ttu-id="421b1-177">`stripPrefix`: logická hodnota, výchozí hodnota je `false`.</span><span class="sxs-lookup"><span data-stu-id="421b1-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="421b1-178">Předchozí kód XML odděluje nastavení aplikace z připojovacích řetězců, ale vyžaduje, aby všechny klíče v souboru *Web. config* používaly zadanou předponu.</span><span class="sxs-lookup"><span data-stu-id="421b1-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="421b1-179">Například `AppSetting` předpony musí být přidány do klíče `ServiceID` ("AppSetting_ServiceID").</span><span class="sxs-lookup"><span data-stu-id="421b1-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="421b1-180">V `stripPrefix`se předpona nepoužívá v souboru *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="421b1-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="421b1-181">Ve zdroji tvůrce konfigurace je vyžadována předpona (například v prostředí). Předpokládáme, že většina vývojářů použije `stripPrefix`.</span><span class="sxs-lookup"><span data-stu-id="421b1-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="421b1-182">Aplikace obvykle vycházejí z předpony.</span><span class="sxs-lookup"><span data-stu-id="421b1-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="421b1-183">Následující soubor *Web. config* vyříznout tuto předponu:</span><span class="sxs-lookup"><span data-stu-id="421b1-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="421b1-184">V předchozím souboru *Web. config* je `default` klíč v `<appSettings/>` i `<connectionStrings/>`.</span><span class="sxs-lookup"><span data-stu-id="421b1-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="421b1-185">Následující obrázek ukazuje `<appSettings/>` a `<connectionStrings/>` klíče/hodnoty z předchozího souboru *Web. config* , který je nastaven v editoru prostředí:</span><span class="sxs-lookup"><span data-stu-id="421b1-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![Editor prostředí](config-builder/static/prefix.png)

<span data-ttu-id="421b1-187">Následující kód přečte `<appSettings/>` a `<connectionStrings/>` klíče/hodnoty obsažené v předchozím souboru *Web. config* :</span><span class="sxs-lookup"><span data-stu-id="421b1-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="421b1-188">Předchozí kód nastaví hodnoty vlastností na:</span><span class="sxs-lookup"><span data-stu-id="421b1-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="421b1-189">Hodnoty v souboru *Web. config* , pokud klíče nejsou nastaveny v proměnných prostředí.</span><span class="sxs-lookup"><span data-stu-id="421b1-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="421b1-190">Hodnoty proměnné prostředí, je-li nastavena.</span><span class="sxs-lookup"><span data-stu-id="421b1-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="421b1-191">Například pomocí předchozího souboru *Web. config* , klíčů/hodnot v předchozí imagi editoru prostředí a předchozího kódu jsou nastaveny následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="421b1-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="421b1-192">Klíč</span><span class="sxs-lookup"><span data-stu-id="421b1-192">Key</span></span>              | <span data-ttu-id="421b1-193">Hodnota</span><span class="sxs-lookup"><span data-stu-id="421b1-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="421b1-194">Idslužby</span><span class="sxs-lookup"><span data-stu-id="421b1-194">ServiceID</span></span>           | <span data-ttu-id="421b1-195">AppSetting_ServiceID z proměnných ENV</span><span class="sxs-lookup"><span data-stu-id="421b1-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="421b1-196">default</span><span class="sxs-lookup"><span data-stu-id="421b1-196">default</span></span>            | <span data-ttu-id="421b1-197">AppSetting_default hodnota z ENV</span><span class="sxs-lookup"><span data-stu-id="421b1-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="421b1-198">default</span><span class="sxs-lookup"><span data-stu-id="421b1-198">default</span></span>         | <span data-ttu-id="421b1-199">ConnStr_default Val ze ENV</span><span class="sxs-lookup"><span data-stu-id="421b1-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="421b1-200">tokenPattern</span><span class="sxs-lookup"><span data-stu-id="421b1-200">tokenPattern</span></span>

<span data-ttu-id="421b1-201">`tokenPattern`: řetězec, výchozí nastavení `@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="421b1-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="421b1-202">Chování `Expand` v sestavách vyhledává nezpracovaný kód XML pro tokeny, které vypadají jako `${token}`.</span><span class="sxs-lookup"><span data-stu-id="421b1-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="421b1-203">Hledání se provádí s výchozím regulárním výrazem `@"\$\{(\w+)\}"`.</span><span class="sxs-lookup"><span data-stu-id="421b1-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="421b1-204">Sada znaků, které odpovídají `\w`, je větší než XML a mnoho zdrojů konfigurace povoluje.</span><span class="sxs-lookup"><span data-stu-id="421b1-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="421b1-205">Pokud název tokenu vyžaduje více znaků, než je `@"\$\{(\w+)\}"`, použijte `tokenPattern`.</span><span class="sxs-lookup"><span data-stu-id="421b1-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="421b1-206">`tokenPattern`: řetězec:</span><span class="sxs-lookup"><span data-stu-id="421b1-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="421b1-207">Umožňuje vývojářům změnit regulární výraz, který se používá pro odpovídající tokeny.</span><span class="sxs-lookup"><span data-stu-id="421b1-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="421b1-208">Neprovádí se žádné ověření, abyste se ujistili, že se jedná o správný regulární výraz, který není bezpečný.</span><span class="sxs-lookup"><span data-stu-id="421b1-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="421b1-209">Musí obsahovat skupinu zachycení.</span><span class="sxs-lookup"><span data-stu-id="421b1-209">It must contain a capture group.</span></span> <span data-ttu-id="421b1-210">Celý regulární výraz se musí shodovat s celým tokenem.</span><span class="sxs-lookup"><span data-stu-id="421b1-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="421b1-211">První zachycení musí být název tokenu, aby bylo možné vyhledat zdroj konfigurace.</span><span class="sxs-lookup"><span data-stu-id="421b1-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="421b1-212">Tvůrci konfigurace v Microsoft. Configuration. ConfigurationBuilders</span><span class="sxs-lookup"><span data-stu-id="421b1-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="421b1-213">EnvironmentConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="421b1-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="421b1-214">[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span><span class="sxs-lookup"><span data-stu-id="421b1-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="421b1-215">Je nejjednodušší pro sestavovatele konfigurace.</span><span class="sxs-lookup"><span data-stu-id="421b1-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="421b1-216">Přečte hodnoty z prostředí.</span><span class="sxs-lookup"><span data-stu-id="421b1-216">Reads values from the environment.</span></span>
* <span data-ttu-id="421b1-217">Nemá žádné další možnosti konfigurace.</span><span class="sxs-lookup"><span data-stu-id="421b1-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="421b1-218">Hodnota atributu `name` je libovolná.</span><span class="sxs-lookup"><span data-stu-id="421b1-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="421b1-219">**Poznámka:** V prostředí kontejneru Windows jsou proměnné nastavené v době běhu vloženy pouze do prostředí procesu EntryPoint.</span><span class="sxs-lookup"><span data-stu-id="421b1-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="421b1-220">Aplikace, které běží jako služba nebo jiný než vstupní bod, nevezmou tyto proměnné, pokud nejsou jinak vloženy pomocí mechanismu v kontejneru.</span><span class="sxs-lookup"><span data-stu-id="421b1-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="421b1-221">V případě kontejnerů založených na [službě IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)aktuální verze [ServiceMonitor. exe](https://github.com/Microsoft/iis-docker/pull/41) zpracovává tuto službu pouze v rámci aplikace *DefaultAppPool* .</span><span class="sxs-lookup"><span data-stu-id="421b1-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="421b1-222">Jiné varianty kontejneru založené na systému Windows můžou potřebovat vyvinout vlastní mechanizmy injektáže pro procesy, které nejsou typu EntryPoint.</span><span class="sxs-lookup"><span data-stu-id="421b1-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="421b1-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="421b1-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="421b1-224">Nikdy neukládejte hesla, citlivé připojovací řetězce ani další citlivá data ve zdrojovém kódu.</span><span class="sxs-lookup"><span data-stu-id="421b1-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="421b1-225">Provozní tajemství by se neměla používat pro vývoj nebo testování.</span><span class="sxs-lookup"><span data-stu-id="421b1-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="421b1-226">Tento nástroj Configuration Manager poskytuje funkci podobnou [ASP.NET Core správce tajných klíčů](/aspnet/core/security/app-secrets).</span><span class="sxs-lookup"><span data-stu-id="421b1-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="421b1-227">[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) se dá použít v projektech .NET Framework, ale musí se zadat soubor tajných klíčů.</span><span class="sxs-lookup"><span data-stu-id="421b1-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="421b1-228">Alternativně můžete definovat vlastnost `UserSecretsId` v souboru projektu a vytvořit nezpracovaný soubor tajných klíčů ve správném umístění pro čtení.</span><span class="sxs-lookup"><span data-stu-id="421b1-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="421b1-229">Chcete-li zachovat externí závislosti mimo váš projekt, tajný soubor je ve formátu XML.</span><span class="sxs-lookup"><span data-stu-id="421b1-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="421b1-230">Formátování XML je podrobné informace o implementaci a formát by neměl spoléhat na.</span><span class="sxs-lookup"><span data-stu-id="421b1-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="421b1-231">Pokud potřebujete sdílet soubor *tajných kódů. JSON* s projekty .NET Core, zvažte použití [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span><span class="sxs-lookup"><span data-stu-id="421b1-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span></span> <span data-ttu-id="421b1-232">Formát `SimpleJsonConfigBuilder` pro .NET Core by měl být také považován za podrobnosti implementace, které se mohou změnit.</span><span class="sxs-lookup"><span data-stu-id="421b1-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="421b1-233">Konfigurační atributy pro `UserSecretsConfigBuilder`:</span><span class="sxs-lookup"><span data-stu-id="421b1-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="421b1-234">`userSecretsId` – jedná se o upřednostňovanou metodu pro identifikaci souboru tajných kódů XML.</span><span class="sxs-lookup"><span data-stu-id="421b1-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="421b1-235">Funguje podobně jako rozhraní .NET Core, které používá vlastnost projektu `UserSecretsId` k uložení tohoto identifikátoru.</span><span class="sxs-lookup"><span data-stu-id="421b1-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="421b1-236">Řetězec musí být jedinečný, nemusí se jednat o identifikátor GUID.</span><span class="sxs-lookup"><span data-stu-id="421b1-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="421b1-237">U tohoto atributu `UserSecretsConfigBuilder` pro soubor tajných kódů patřící k tomuto identifikátoru najít dobře známé místní umístění (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`).</span><span class="sxs-lookup"><span data-stu-id="421b1-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="421b1-238">`userSecretsFile` – volitelný atribut určující soubor obsahující tajné klíče.</span><span class="sxs-lookup"><span data-stu-id="421b1-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="421b1-239">`~` znak lze použít na začátku pro odkaz na kořen aplikace.</span><span class="sxs-lookup"><span data-stu-id="421b1-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="421b1-240">Je vyžadován buď tento atribut, nebo atribut `userSecretsId`.</span><span class="sxs-lookup"><span data-stu-id="421b1-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="421b1-241">Pokud jsou zadány obě, má `userSecretsFile` přednost.</span><span class="sxs-lookup"><span data-stu-id="421b1-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="421b1-242">`optional`: Boolean, výchozí hodnota `true` – zabrání výjimce, pokud nebyl nalezen soubor tajných klíčů.</span><span class="sxs-lookup"><span data-stu-id="421b1-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="421b1-243">Hodnota atributu `name` je libovolná.</span><span class="sxs-lookup"><span data-stu-id="421b1-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="421b1-244">Soubor tajných kódů má následující formát:</span><span class="sxs-lookup"><span data-stu-id="421b1-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="421b1-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="421b1-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="421b1-246">[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) čte hodnoty uložené v [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="421b1-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="421b1-247">`vaultName` se vyžaduje (buď název trezoru, nebo identifikátor URI k trezoru).</span><span class="sxs-lookup"><span data-stu-id="421b1-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="421b1-248">Ostatní atributy umožňují řízení, ke kterému trezoru se má připojit, ale jsou nezbytné pouze v případě, že aplikace neběží v prostředí, které funguje s `Microsoft.Azure.Services.AppAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="421b1-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="421b1-249">Knihovna ověřování služeb Azure slouží k automatickému výběru informací o připojení z prováděcího prostředí, pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="421b1-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="421b1-250">K automatickému výběru informací o připojení můžete potlačit zadáním připojovacího řetězce.</span><span class="sxs-lookup"><span data-stu-id="421b1-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="421b1-251">`vaultName` – vyžaduje se, pokud `uri` není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="421b1-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="421b1-252">Určuje název trezoru v předplatném Azure, ze kterého se mají číst páry klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="421b1-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="421b1-253">`connectionString` – připojovací řetězec použitelný pomocí [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span><span class="sxs-lookup"><span data-stu-id="421b1-253">`connectionString` - A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* <span data-ttu-id="421b1-254">`uri` – připojuje se k jiným poskytovatelům Key Vault se zadanou `uri` hodnotou.</span><span class="sxs-lookup"><span data-stu-id="421b1-254">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="421b1-255">Pokud není zadaný, Azure (`vaultName`) je poskytovatelem trezoru.</span><span class="sxs-lookup"><span data-stu-id="421b1-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="421b1-256">`version`-Azure Key Vault poskytuje funkci správy verzí tajných kódů.</span><span class="sxs-lookup"><span data-stu-id="421b1-256">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="421b1-257">Je-li zadán `version`, tvůrce načte pouze tajné kódy, které odpovídají této verzi.</span><span class="sxs-lookup"><span data-stu-id="421b1-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="421b1-258">`preloadSecretNames` – ve výchozím nastavení bude tento tvůrce dotazovat **všechny** názvy klíčů v trezoru klíčů při inicializaci.</span><span class="sxs-lookup"><span data-stu-id="421b1-258">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="421b1-259">Chcete-li zabránit čtení všech hodnot klíče, nastavte tento atribut na `false`.</span><span class="sxs-lookup"><span data-stu-id="421b1-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="421b1-260">Když toto nastavení nastavíte na `false` přečtou tajné klíče po jednom.</span><span class="sxs-lookup"><span data-stu-id="421b1-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="421b1-261">Čtení tajných kódů po jednom může být užitečné, pokud trezor umožňuje přístup "získat", ale ne "seznam".</span><span class="sxs-lookup"><span data-stu-id="421b1-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="421b1-262">**Poznámka:** Při použití režimu `Greedy` musí být `preloadSecretNames` `true` (výchozí nastavení).</span><span class="sxs-lookup"><span data-stu-id="421b1-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="421b1-263">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="421b1-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="421b1-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) je základní nástroj Configuration Builder, který jako zdroj hodnot používá soubory adresáře.</span><span class="sxs-lookup"><span data-stu-id="421b1-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="421b1-265">Název souboru je klíč a obsah je hodnota.</span><span class="sxs-lookup"><span data-stu-id="421b1-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="421b1-266">Tento nástroj Configuration Builder může být užitečný při spuštění v prostředí orchestrace kontejnerů.</span><span class="sxs-lookup"><span data-stu-id="421b1-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="421b1-267">Systémy, jako jsou Docker Swarm a Kubernetes, poskytují `secrets` do jejich orchestrace kontejnerů Windows v tomto způsobu souboru pro daný klíč.</span><span class="sxs-lookup"><span data-stu-id="421b1-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="421b1-268">Podrobnosti atributu:</span><span class="sxs-lookup"><span data-stu-id="421b1-268">Attribute details:</span></span>

* <span data-ttu-id="421b1-269">`directoryPath` – povinné.</span><span class="sxs-lookup"><span data-stu-id="421b1-269">`directoryPath` - Required.</span></span> <span data-ttu-id="421b1-270">Určuje cestu pro hledání hodnot.</span><span class="sxs-lookup"><span data-stu-id="421b1-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="421b1-271">Docker for Windows tajné klíče jsou ve výchozím nastavení ukládány do adresáře *C:\ProgramData\Docker\secrets* .</span><span class="sxs-lookup"><span data-stu-id="421b1-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="421b1-272">`ignorePrefix` – soubory, které začínají touto předponou, jsou vyloučené.</span><span class="sxs-lookup"><span data-stu-id="421b1-272">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="421b1-273">Výchozí hodnota je ignore.</span><span class="sxs-lookup"><span data-stu-id="421b1-273">Defaults to "ignore.".</span></span>
* <span data-ttu-id="421b1-274">`keyDelimiter` – výchozí hodnota je `null`.</span><span class="sxs-lookup"><span data-stu-id="421b1-274">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="421b1-275">Je-li tento parametr zadán, projde nástroj Configuration Builder více úrovní adresáře a sestaví názvy klíčů pomocí tohoto oddělovače.</span><span class="sxs-lookup"><span data-stu-id="421b1-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="421b1-276">Pokud je tato hodnota `null`, nástroj Configuration Builder se vyhledá jenom na nejvyšší úrovni adresáře.</span><span class="sxs-lookup"><span data-stu-id="421b1-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="421b1-277">`optional` – výchozí hodnota je `false`.</span><span class="sxs-lookup"><span data-stu-id="421b1-277">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="421b1-278">Určuje, zda má nástroj Configuration Builder způsobit chyby v případě, že zdrojový adresář neexistuje.</span><span class="sxs-lookup"><span data-stu-id="421b1-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="421b1-279">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="421b1-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="421b1-280">Nikdy neukládejte hesla, citlivé připojovací řetězce ani další citlivá data ve zdrojovém kódu.</span><span class="sxs-lookup"><span data-stu-id="421b1-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="421b1-281">Provozní tajemství by se neměla používat pro vývoj nebo testování.</span><span class="sxs-lookup"><span data-stu-id="421b1-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="421b1-282">Projekty .NET Core často používají soubory JSON pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="421b1-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="421b1-283">Tvůrce [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) umožňuje používat v .NET Framework soubory JSON pro .NET Core.</span><span class="sxs-lookup"><span data-stu-id="421b1-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="421b1-284">Tento nástroj Configuration Builder poskytuje základní mapování ze zdroje nestrukturovaných klíčů a hodnot do konkrétních oblastí s klíči a hodnotami konfigurace .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="421b1-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="421b1-285">Tento nástroj Configuration Builder **neposkytuje hierarchické** konfigurace.</span><span class="sxs-lookup"><span data-stu-id="421b1-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="421b1-286">Soubor zálohy JSON je podobný slovníku, nikoli složitému hierarchickému objektu.</span><span class="sxs-lookup"><span data-stu-id="421b1-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="421b1-287">Můžete použít hierarchický soubor s více úrovněmi.</span><span class="sxs-lookup"><span data-stu-id="421b1-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="421b1-288">Tento poskytovatel `flatten`s hloubkou připojením názvu vlastnosti na všech úrovních pomocí `:` jako oddělovače.</span><span class="sxs-lookup"><span data-stu-id="421b1-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="421b1-289">Podrobnosti atributu:</span><span class="sxs-lookup"><span data-stu-id="421b1-289">Attribute details:</span></span>

* <span data-ttu-id="421b1-290">`jsonFile` – povinné.</span><span class="sxs-lookup"><span data-stu-id="421b1-290">`jsonFile` - Required.</span></span> <span data-ttu-id="421b1-291">Určuje soubor JSON, ze kterého se má číst.</span><span class="sxs-lookup"><span data-stu-id="421b1-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="421b1-292">`~` znak lze použít na začátku pro odkaz na kořen aplikace.</span><span class="sxs-lookup"><span data-stu-id="421b1-292">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="421b1-293">`optional` – logická hodnota, výchozí hodnota je `true`.</span><span class="sxs-lookup"><span data-stu-id="421b1-293">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="421b1-294">Zabraňuje vyvolání výjimek, pokud nelze najít soubor JSON.</span><span class="sxs-lookup"><span data-stu-id="421b1-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="421b1-295">`jsonMode` - `[Flat|Sectional]`.</span><span class="sxs-lookup"><span data-stu-id="421b1-295">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="421b1-296">`Flat` je výchozí možnost.</span><span class="sxs-lookup"><span data-stu-id="421b1-296">`Flat` is the default.</span></span> <span data-ttu-id="421b1-297">Je-li `jsonMode` `Flat`, je soubor JSON jedním zdrojem nestrukturovaných klíč/hodnota.</span><span class="sxs-lookup"><span data-stu-id="421b1-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="421b1-298">`EnvironmentConfigBuilder` a `AzureKeyVaultConfigBuilder` jsou také jedním nestrukturovaným zdrojem klíčů a hodnot.</span><span class="sxs-lookup"><span data-stu-id="421b1-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="421b1-299">Když je `SimpleJsonConfigBuilder` nakonfigurovaný v režimu `Sectional`:</span><span class="sxs-lookup"><span data-stu-id="421b1-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="421b1-300">Soubor JSON je koncepčně rozdělený přímo na nejvyšší úrovni do více slovníků.</span><span class="sxs-lookup"><span data-stu-id="421b1-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="421b1-301">Každý ze slovníků je použit pouze pro konfigurační oddíl, který odpovídá názvu vlastnosti nejvyšší úrovně, který je k nim připojen.</span><span class="sxs-lookup"><span data-stu-id="421b1-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="421b1-302">Příklad:</span><span class="sxs-lookup"><span data-stu-id="421b1-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="421b1-303">Implementace vlastního tvůrce konfigurace klíčů a hodnot</span><span class="sxs-lookup"><span data-stu-id="421b1-303">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="421b1-304">Pokud konfigurační tvůrci nevyhovují vašim potřebám, můžete napsat vlastní.</span><span class="sxs-lookup"><span data-stu-id="421b1-304">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="421b1-305">`KeyValueConfigBuilder` základní třída zpracovává substituční režimy a většinu otázek.</span><span class="sxs-lookup"><span data-stu-id="421b1-305">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="421b1-306">Implementující projekt vyžaduje jenom:</span><span class="sxs-lookup"><span data-stu-id="421b1-306">An implementing project need only:</span></span>

* <span data-ttu-id="421b1-307">Dědí ze základní třídy a implementuje základní zdroj párů klíč/hodnota prostřednictvím `GetValue` a `GetAllValues`:</span><span class="sxs-lookup"><span data-stu-id="421b1-307">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="421b1-308">Přidejte do projektu [Microsoft. Configuration. ConfigurationBuilders. Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) .</span><span class="sxs-lookup"><span data-stu-id="421b1-308">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="421b1-309">`KeyValueConfigBuilder` základní třída poskytuje mnoho práce a konzistentní chování napříč sestavami konfigurace klíčů a hodnot.</span><span class="sxs-lookup"><span data-stu-id="421b1-309">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="421b1-310">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="421b1-310">Additional resources</span></span>

* [<span data-ttu-id="421b1-311">Úložiště GitHubu pro sestavovatele konfigurace</span><span class="sxs-lookup"><span data-stu-id="421b1-311">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="421b1-312">Ověřování služba-služba pro Azure Key Vault pomocí .NET</span><span class="sxs-lookup"><span data-stu-id="421b1-312">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)

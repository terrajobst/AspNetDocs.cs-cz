---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET – rychlý přehled rozhraní API pro webové stránky (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tato stránka obsahuje seznam obsahující stručné příklady nejčastěji používaných objektů, vlastností a metod pro programování webových stránek ASP.NET pomocí syntaxe Razor.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574331"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET API Web Pages (Razor) – rychlý přehled

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tato stránka obsahuje seznam obsahující stručné příklady nejčastěji používaných objektů, vlastností a metod pro programování webových stránek ASP.NET pomocí syntaxe Razor.
> 
> Popisy označené "(v2)" byly představeny ve webových stránkách ASP.NET verze 2.
> 
> Referenční dokumentaci k rozhraní API najdete v [referenční dokumentaci k webovým stránkám ASP.NET](https://go.microsoft.com/fwlink/?LinkId=208659) na webu MSDN.
> 
> ## <a name="software-versions"></a>Verze softwaru
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz taky funguje s ASP.NET webovými stránkami 2 a ASP.NET Web Pages 1,0 (s výjimkou funkcí označených jako v2).

Tato stránka obsahuje referenční informace pro následující:

- [Třídy](#Classes)
- [Data](#Data)
- [Pomocné rutiny](#Helpers)
- [Ověřování](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>Třídy

### `AppState[key], AppState[index],App`

Obsahuje data, která lze sdílet se všemi stránkami aplikace. Vlastnost Dynamic `App` můžete použít pro přístup ke stejným datům, jako v následujícím příkladu:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

Převede hodnotu řetězce na logickou hodnotu (true/false). Vrátí hodnotu false nebo zadanou hodnotu, pokud řetězec nepředstavuje hodnotu true nebo false.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

Převede hodnotu řetězce na datum a čas. Vrátí `DateTime.MinValue` nebo zadanou hodnotu, pokud řetězec nepředstavuje datum a čas.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

Převede hodnotu řetězce na desítkovou hodnotu. Vrátí 0,0 nebo zadanou hodnotu, pokud řetězec nepředstavuje desítkovou hodnotu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

Převede řetězcovou hodnotu na float. Vrátí 0,0 nebo zadanou hodnotu, pokud řetězec nepředstavuje desítkovou hodnotu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

Převede řetězcovou hodnotu na celé číslo. Vrátí hodnotu 0 nebo zadanou hodnotu, pokud řetězec nepředstavuje celé číslo.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

Vytvoří adresu URL kompatibilní s prohlížečem z místní cesty k souboru s volitelnými dalšími částmi cesty.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

Vykresluje *hodnotu* jako značku HTML místo vykreslování jako výstup kódovaný ve formátu HTML.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

Vrátí hodnotu true, pokud může být hodnota převedena z řetězce na zadaný typ.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

Vrátí hodnotu true, pokud objekt nebo proměnná nemá žádnou hodnotu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

Vrátí hodnotu true, pokud je požadavek POST. (Počáteční požadavky jsou obvykle GET.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

Určuje cestu stránky rozložení, která se má použít na tuto stránku.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

Obsahuje data sdílená mezi stránkou, stránkami rozložení a částečnými stránkami v rámci aktuálního požadavku. Vlastnost Dynamic `Page` můžete použít pro přístup ke stejným datům, jako v následujícím příkladu:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(Stránky rozložení) Vykreslí obsah stránky obsahu, která není v žádné z pojmenovaných sekcí.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

Vykreslí stránku obsahu pomocí zadané cesty a nepovinných dat navíc. Hodnoty dalších parametrů můžete získat z `PageData` podle pozice (Příklad 1) nebo klíče (příklad 2).

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(Stránky rozložení) Vykreslí oddíl obsahu s názvem. Nastavte na hodnotu false, *Pokud chcete,* aby byla sekce volitelná.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

Získá nebo nastaví hodnotu souboru cookie protokolu HTTP.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

Načte soubory, které byly odeslány v rámci aktuálního požadavku.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

Načte data, která byla publikována ve formuláři (jako řetězce). `Request[key]` kontroluje `Request.Form` i kolekce `Request.QueryString`.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

Načte data zadaná v řetězci dotazu URL. `Request[key]` kontroluje `Request.Form` i kolekce `Request.QueryString`.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

Selektivně zakáže ověření žádosti pro element formuláře, hodnotu řetězce dotazu, soubor cookie nebo hodnotu hlavičky. Ověření žádosti je ve výchozím nastavení povolené a brání uživatelům v odesílání značek nebo jiného potenciálně nebezpečného obsahu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

Přidá hlavičku serveru HTTP do odpovědi.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

Uloží výstup stránky do mezipaměti po určitou dobu. Volitelně můžete nastavit možnost *klouzavého* intervalu pro resetování časového limitu při přístupu každé stránky a přihlašování do *mezipaměti pro každý* jiný řetězec dotazu v žádosti stránky ukládat do mezipaměti různé verze stránky.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

Přesměruje požadavek prohlížeče na nové umístění.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

Nastaví stavový kód protokolu HTTP odeslaný do prohlížeče.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

Zapíše obsah *dat* do odpovědi pomocí volitelného typu MIME.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

Zapíše obsah souboru do odpovědi.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(Stránky rozložení) Definuje oddíl obsahu, který má název.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

Dekóduje řetězec, který je kódovaný v jazyce HTML.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

Zakóduje řetězec pro vykreslování v kódu HTML.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

Vrátí fyzickou cestu serveru pro zadanou virtuální cestu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

Dekóduje text z adresy URL.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

Zakóduje text, který se vloží do adresy URL.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

Získá nebo nastaví hodnotu, která existuje, dokud uživatel nezavře prohlížeč.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

Zobrazí řetězcovou reprezentaci hodnoty objektu.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

Získá další data z adresy URL (například */MyPage/ExtraData*).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

Změní heslo pro zadaného uživatele.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

Potvrdí účet pomocí potvrzovacího tokenu účtu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

Vytvoří nový uživatelský účet se zadaným uživatelským jménem a heslem. Chcete-li vyžadovat potvrzovací token, předejte hodnotu true pro *requireConfirmationToken.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

Získá celočíselný identifikátor aktuálně přihlášeného uživatele.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

Získá jméno aktuálně přihlášeného uživatele.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

Vygeneruje token pro resetování hesla, který se dá odeslat e-mailem uživateli, aby uživatel mohl heslo resetovat.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

Vrátí ID uživatele z uživatelského jména.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

Vrátí hodnotu true, pokud je aktuální uživatel přihlášen.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

Vrátí hodnotu pravda, pokud byl uživatel potvrzen (například prostřednictvím potvrzovacího e-mailu).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

Vrátí hodnotu pravda, pokud jméno aktuálního uživatele odpovídá zadanému uživatelskému jménu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

Zaznamená uživatele v nástroji nastavením ověřovacího tokenu v souboru cookie.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

Odhlásí uživatele odebráním souboru cookie ověřovacího tokenu.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

Pokud není uživatel ověřen, nastaví stav protokolu HTTP na 401 (neautorizováno).

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

Pokud aktuální uživatel není členem jedné ze zadaných rolí, nastaví stav HTTP na 401 (Neautorizováno).

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

Pokud aktuální uživatel není uživatelem zadaný pomocí *uživatelského jména*, nastaví stav HTTP na 401 (Neautorizováno).

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

Pokud je token pro resetování hesla platný, změní heslo uživatele na nové heslo.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>Data

### `Database.Execute(SQLstatement [,parameters]`

Spustí *SQLstatement* (s nepovinnými parametry), jako je například INSERT, DELETE nebo Update a vrátí počet ovlivněných záznamů.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

Vrátí sloupec identity z naposledy vloženého řádku.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

Otevře buď zadaný databázový soubor, nebo databázi zadanou pomocí pojmenovaného připojovacího řetězce ze souboru *Web. config* .

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

Otevře databázi pomocí připojovacího řetězce. (To se liší od `Database.Open`, která používá název připojovacího řetězce.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

Dotazuje databázi pomocí *SQLstatement* (volitelně předáním parametrů) a vrátí výsledky jako kolekci.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

Spustí *SQLstatement* (s nepovinnými parametry) a vrátí jeden záznam.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

Spustí *SQLstatement* (s nepovinnými parametry) a vrátí jedinou hodnotu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>Pomocné rutiny

### `Analytics.GetGoogleHtml(webPropertyId)`

Vykreslí kód JavaScriptu pro Google Analytics pro zadané ID.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

Vykreslí kód JavaScriptu StatCounter Analytics pro zadaný projekt.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

Vykreslí kód JavaScriptu pro Yahoo Analytics pro zadaný účet.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Předá vyhledávání Bingu. Chcete-li určit web, který chcete vyhledat, a název vyhledávacího pole, můžete nastavit `Bing.SiteUrl` a vlastnosti `Bing.SiteTitle`. Tyto vlastnosti se obvykle nastavují na stránce *\_AppStart* .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

Inicializuje graf.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

Přidá legendu do grafu.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

Přidá do grafu řadu hodnot.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

Vrátí hodnotu hash pro zadaná data. Výchozí algoritmus je `sha256`.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Umožňuje uživatelům Facebooku navázání připojení k stránkám.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

Vykreslí uživatelské rozhraní pro nahrávání souborů.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

Vykreslí určenou značku Xbox hráčských.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

Vykreslí Gravatar obrázek pro zadanou e-mailovou adresu.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

Převede datový objekt na řetězec ve formátu JavaScript Object Notation (JSON).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

Převede vstupní řetězec kódovaný ve formátu JSON na datový objekt, který můžete iterovat nebo vložit do databáze.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

Vykresluje odkazy na sociální sítě pomocí zadaného názvu a volitelné adresy URL.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

Přidruží k chybové zprávě pole formuláře. Pro přístup k tomuto členu použijte pomoc `ModelState`.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

Přidruží k chybě zprávu s formulářem. Pro přístup k tomuto členu použijte pomoc `ModelState`.

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

Vrátí hodnotu true, pokud nedošlo k chybám ověření. Pro přístup k tomuto členu použijte pomoc `ModelState`.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

Vykreslí vlastnosti a hodnoty objektu a všech podřízených objektů.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

Vykreslí ověřovací test reCAPTCHA.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

Nastaví veřejné a privátní klíče pro službu reCAPTCHA. Tyto vlastnosti se obvykle nastavují na stránce *\_AppStart* .

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

Vrátí výsledek testu reCAPTCHA.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

Vykresluje informace o stavu webových stránek ASP.NET.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

Vykreslí datový proud Twitteru pro zadaného uživatele.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

Vykreslí datový proud Twitteru pro zadaný hledaný text.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

Vykreslí video přehrávač Flash pro zadaný soubor s volitelnou šířkou a výškou.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

Vykreslí přehrávač Windows Media Player pro zadaný soubor s volitelnou šířkou a výškou.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

Vykreslí přehrávač Silverlight pro zadaný soubor *. xap* s požadovanou šířkou a výškou.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

Vrátí objekt určený *klíčovou*hodnotou nebo hodnotu null, pokud objekt nebyl nalezen.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

Odebere objekt určený *klíčem* z mezipaměti.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

Vloží *hodnotu* do mezipaměti pod názvem zadaným *klíčem*.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

Vytvoří nový objekt `WebGrid` s využitím dat z dotazu.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

Vykreslí označení pro zobrazení dat v tabulce HTML.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

Vykreslí pager pro objekt `WebGrid`.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

Načte obrázek ze zadané cesty.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

Přidá zadaný obrázek jako vodoznak.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

Přidá zadaný text do obrázku.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

Překlopí obrázek vodorovně nebo svisle.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

Načte obrázek, když se na stránku při nahrání souboru publikuje obrázek.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

Změní velikost obrázku.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

Otočí obrázek doleva nebo doprava.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

Uloží obrázek do zadané cesty.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

Nastaví heslo pro server SMTP. Obvykle tuto vlastnost nastavíte na stránce *\_AppStart* .

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

Pošle e-mailovou zprávu.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

Nastaví název serveru SMTP. Obvykle tuto vlastnost nastavíte na stránce *\_AppStart* .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

Nastaví uživatelské jméno pro server SMTP. Obvykle byste tuto vlastnost měli nastavit na stránce *\_AppStart* .

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>Ověření

### `Html.ValidationMessage(field)`

2 Vykreslí chybovou zprávu ověřování pro zadané pole.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

2 Zobrazí seznam všech chyb ověřování.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

2 Zaregistruje element vstupu uživatele pro zadaný typ ověřování.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

2 Dynamicky vykresluje atributy třídy CSS pro ověřování na straně klienta, aby bylo možné formátovat chybové zprávy ověřování. (Vyžaduje, abyste odkazovali na příslušné knihovny klientského skriptu a definovali třídy CSS.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

2 Povolí ověřování na straně klienta pro vstupní pole uživatele. (Vyžaduje, abyste odkazovali na příslušné knihovny skriptu klienta.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

2 Vrátí hodnotu true, pokud všechny prvky vstupu uživatele, které jsou registred pro ověření, obsahují platné hodnoty.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

2 Určuje, že uživatelé musí zadat hodnotu pro prvek vstupu uživatele.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

2 Určuje, že uživatelé musí zadat hodnoty pro každý prvek vstupu uživatele. Tato metoda neumožňuje zadat vlastní chybovou zprávu.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

2 Určuje ověřovací test při použití metody `Validation.Add`.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]

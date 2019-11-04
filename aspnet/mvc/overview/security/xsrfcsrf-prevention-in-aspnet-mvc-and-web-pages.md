---
uid: mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
title: Prevence XSRF/CSRF v ASP.NET MVC a webových stránkách | Microsoft Docs
author: Rick-Anderson
description: Padělání žádostí mezi weby (označované také jako XSRF nebo CSRF) představuje útok proti aplikacím hostovaným na webu, kde může škodlivý web ovlivnit interakci...
ms.author: riande
ms.date: 03/14/2013
ms.assetid: aadc5fa4-8215-4fc7-afd5-bcd2ef879728
msc.legacyurl: /mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
msc.type: authoredcontent
ms.openlocfilehash: 6fcfcda5b95e5844f7d357ac0cbb6d1fd2e215ac
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445766"
---
# <a name="xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages"></a>Prevence XSRF/CSRF v ASP.NET MVC a na webových stránkách

Od [Rick Anderson]((https://twitter.com/RickAndMSFT))

> Padělání žádostí mezi weby (označované také jako XSRF nebo CSRF) představuje útok proti aplikacím hostovaným na webu, kdy škodlivý web může ovlivnit interakci mezi klientským prohlížečem a webem, který tento prohlížeč důvěřuje. Tyto útoky byly umožněny, protože webové prohlížeče budou automaticky odesílat ověřovací tokeny s každým požadavkem na web. Kanonický příklad je ověřovací soubor cookie, jako je například ASP. Lístek pro ověřování formulářů netto. Tyto útoky ale můžou cílit na weby, které používají jakýkoliv mechanismus trvalého ověřování (například ověřování systému Windows, Basic a tak dále).
> 
> Útok XSRF se liší od útoku phishing. Útoky typu phishing vyžadují interakci od oběti. V útokech na útok phishing se škodlivý web napodobá cílovému webu a oběť se na něj zahájí poskytování citlivých informací útočníkovi. V útoku XSRF není často potřeba žádná interakce od oběti. Místo toho se útočník spoléhá na to, že prohlížeč automaticky posílá všechny relevantní soubory cookie do cílového webu.
> 
> Další informace naleznete v tématu [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page)(OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)).

## <a name="anatomy-of-an-attack"></a>Anatomie útoku

Pokud chcete projít útokem XSRF, vezměte v úvahu uživatele, který chce provést některé online bankovní transakce. Tento uživatel nejdřív navštíví WoodgroveBank.com a přihlásí se. v takovém případě bude hlavička odpovědi obsahovat ověřovací soubor cookie:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample1.cmd)]

Vzhledem k tomu, že soubor cookie ověřování je soubor cookie relace, bude při ukončení procesu prohlížeče automaticky vymazán prohlížečem. Do té doby ale bude prohlížeč automaticky zahrnovat soubor cookie s každým požadavkem na WoodgroveBank.com. Uživatel teď chce přenést $1000 na jiný účet, takže vyplní formulář na bankovním webu a prohlížeč tento požadavek provede na server:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample2.cmd)]

Vzhledem k tomu, že tato operace má vedlejší efekt (iniciuje peněžní transakce), banka se pro zahájení této operace rozhodla vyžadovat požadavek HTTP POST. Server přečte ověřovací token z požadavku, vyhledá číslo účtu uživatele, ověří, že existuje dostatek prostředků, a pak transakci inicializuje do cílového účtu.

Její online banka je dokončena, uživatel přejde pryč z bankovního serveru a navštíví další místa na webu. Jedna z těchto lokalit – fabrikam.com – obsahuje následující značky na stránce vložené do &lt;IFRAME&gt;:

[!code-html[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample3.html)]

To následně způsobí, že prohlížeč tuto žádost provede:

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample4.cmd)]

Útočník zneužije skutečnost, že uživatel může mít stále platný ověřovací token pro cílový web, a používá malý fragment kódu JavaScriptu, který způsobí, že prohlížeč vytvoří automaticky příspěvek HTTP do cílové lokality. Pokud je ověřovací token stále platný, bude bankovní web iniciovat přenos $250 na účet výběru útočníka.

### <a name="ineffective-mitigations"></a>Neúčinná omezení

Je zajímavá Poznámka, že ve výše uvedeném scénáři byl přístup k WoodgroveBank.com přes SSL a že soubor cookie pro ověřování pouze SSL nebyl pro vzdoruje útok nedostatečný. Útočník může v jeho &lt;&gt; elementu zadat [schéma identifikátoru URI](http://en.wikipedia.org/wiki/URI_scheme) (https) a prohlížeč bude nadále odesílat soubory cookie s neplatnými hodnotami do cílové lokality, pokud jsou tyto soubory cookie konzistentní se SCHÉMATem identifikátoru URI zamýšleného cíle.

Jedna z nich by mohla tvrdí, že by uživatel neměl navštěvovat nedůvěryhodné lokality, protože navštěvují jenom důvěryhodné weby, což může zůstat v bezpečí online. Je to pro vás něco pravdy, ale tato doporučení nejsou vždycky praktická. Například uživatel "důvěřuje" místnímu webu novinek ConsolidatedMessenger. ConsolidatedMessenger.com a přejde k návštěvě tohoto webu, ale tato lokalita má zranitelnost XSS, která útočníkovi umožňuje vložit stejný fragment kódu, který běžel v fabrikam.com.

Můžete ověřit, že příchozí požadavky mají v [dokumentaci](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) k vaší doméně referenční hlavičku. Tím se zastaví požadavky unwittingly odeslané z domény třetí strany. Někteří lidé ale z důvodů ochrany osobních údajů zakázali hlavičku tohoto prohlížeče v prohlížeči a útočníci můžou v případě, že má poškozený nějaký nezabezpečený software, někdy tuto hlavičku falešné. Ověření [záhlaví odkazujícího](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) nástroje není považováno za zabezpečený přístup k prevenci útoků XSRF.

## <a name="web-stack-runtime-xsrf-mitigations"></a>Zmírnění rizik v modulu runtime webového zásobníku

Modul runtime webového zásobníku ASP.NET používá variantu [vzoru tokenu synchronizátoru](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#synchronizer-token-pattern) k obraně před útoky XSRF. Základní forma vzoru tokenu synchronizátoru je, že se na server odesílají dva tokeny anti-XSRF (kromě ověřovacího tokenu): jeden token jako soubor cookie a druhý jako hodnota formuláře. Hodnoty tokenu generované modulem runtime ASP.NET nejsou tímto útočníkem deterministické ani předvídatelné. Po odeslání tokenů Server umožní, aby žádost pokračovala pouze v případě, že obě tokeny přejdou kontrolu porovnání.

*Token relace* ověření požadavku XSRF je uložený jako soubor cookie http a v současné době obsahuje následující informace:

- Token zabezpečení, který se skládá z náhodného 128 identifikátoru.   
 Na následujícím obrázku vidíte token relace žádosti XSRF, který je zobrazený pomocí nástrojů pro vývojáře v Internet Exploreru F12: (Všimněte si, že se jedná o aktuální implementaci a že je předmětný, i když se může změnit.)

![](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/_static/image1.png)

*Token pole* je uložen jako `<input type="hidden" />` a ve své datové části obsahuje následující informace:

- Uživatelské jméno přihlášeného uživatele (Pokud je ověřeno).
- Všechna další data, která poskytuje [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx).

Datové části tokenů anti-XSRF jsou šifrované a podepsané, takže nemůžete zobrazit uživatelské jméno při použití nástrojů k prohlédnutí tokenů. Pokud je webová aplikace cílena na ASP.NET 4,0, kryptografické služby jsou k dispozici pomocí rutiny [machineKey. Encode](https://msdn.microsoft.com/library/system.web.security.machinekey.encode.aspx) . Pokud je webová aplikace cílena na ASP.NET 4,5 nebo vyšší, kryptografické služby jsou poskytovány rutinou [machineKey. Protect](https://msdn.microsoft.com/library/system.web.security.machinekey.protect(v=vs.110)) , která nabízí lepší výkon, rozšiřitelnost a zabezpečení. Další podrobnosti najdete v následujících blogových příspěvcích:

- [Vylepšení kryptografie v ASP.NET 4,5, PT. 1](https://blogs.msdn.com/b/webdev/archive/2012/10/22/cryptographic-improvements-in-asp-net-4-5-pt-1.aspx)
- [Vylepšení kryptografie v ASP.NET 4,5, PT. 2](https://blogs.msdn.com/b/webdev/archive/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2.aspx)
- [Vylepšení kryptografie v ASP.NET 4,5, PT. 3](https://blogs.msdn.com/b/webdev/archive/2012/10/24/cryptographic-improvements-in-asp-net-4-5-pt-3.aspx)

## <a name="generating-the-tokens"></a>Generování tokenů

Chcete-li generovat tokeny anti-XSRF, zavolejte metodu [@Html.AntiForgeryToken](https://msdn.microsoft.com/library/dd470175.aspx) ze zobrazení MVC nebo @AntiForgery.GetHtml() ze stránky Razor. Runtime pak provede následující kroky:

1. Pokud aktuální požadavek HTTP již obsahuje token relace anti-XSRF (soubor cookie anti-XSRF \_\_RequestVerificationToken), z něj je extrahován token zabezpečení. Pokud požadavek HTTP neobsahuje token relace anti-XSRF nebo pokud se nezdařila extrakce tokenu zabezpečení, vygeneruje se nový náhodný token anti-XSRF.
2. Token pole anti-XSRF se vygeneruje pomocí tokenu zabezpečení z kroku (1) výše a identity aktuálně přihlášeného uživatele. (Další informace o určování identity uživatele najdete v části **[scénáře s speciální podporou](#_Scenarios_with_special)** níže.) Kromě toho, pokud je nakonfigurován [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/jj158328(v=vs.111).aspx) , modul runtime zavolá svou metodu [GetAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.getadditionaldata(v=vs.111).aspx) a zahrne vrácený řetězec do tokenu pole. (Další informace najdete v části **[Konfigurace a rozšiřitelnost](#_Configuration_and_extensibility)** .)
3. Pokud se nový token anti-XSRF vygeneroval v kroku (1), vytvoří se nový token relace, který bude obsahovat a přidá se do kolekce odchozích souborů cookie HTTP. Token pole z kroku (2) bude zabalen do prvku `<input type="hidden" />` a tento kód HTML bude návratovou hodnotou `Html.AntiForgeryToken()` nebo `AntiForgery.GetHtml()`.

## <a name="validating-the-tokens"></a>Ověřování tokenů

Aby bylo možné ověřit příchozí tokeny anti-XSRF, vývojář zahrne atribut [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(VS.108).aspx) na svou akci nebo kontroler MVC, nebo volá `@AntiForgery.Validate()` ze své stránky Razor. Modul runtime provede následující kroky:

1. Načte se token příchozí relace a token pole a z každého se Extrahuj token anti-XSRF. Tokeny anti-XSRF musí být identické pro každý krok (2) v rutině generování.
2. Pokud je aktuální uživatel ověřený, jeho uživatelské jméno je porovnáno s uživatelským jménem uloženým v tokenu pole. Uživatelská jména se musí shodovat.
3. Pokud je nakonfigurován [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) , modul runtime volá svou metodu *ValidateAdditionalData* . Metoda musí vracet logickou hodnotu *true*.

V případě úspěšného ověření může požadavek pokračovat. Pokud se ověření nezdaří, rozhraní vyvolá výjimku *HttpAntiForgeryException*.

## <a name="failure-conditions"></a>Podmínky selhání

Počínaje modulem runtime webového zásobníku ASP.NET v2 všechny *HttpAntiForgeryException* , které jsou vyvolány během ověřování, budou obsahovat podrobné informace o tom, co se nepovedlo. Aktuálně definované podmínky selhání jsou:

- Token relace nebo token formuláře v žádosti chybí.
- Token relace nebo token formuláře jsou nečitelný. Nejpravděpodobnější příčinou je, že farma používá neshodné verze ASP.NET webového zásobníku nebo farmy, kde se prvek &lt;machineKey&gt; v souboru Web. config liší mezi počítači. Pomocí nástroje, jako je například Fiddler, můžete tuto výjimku vynutit manipulací s tokenem anti-XSRF.
- Token relace a token pole byly prohozeny.
- Token relace a token pole obsahují neshodné tokeny zabezpečení.
- Uživatelské jméno vložené v tokenu pole se neshoduje s aktuálním uživatelským jménem přihlášeného uživatele.
- Metoda *[IAntiForgeryAdditionalDataProvider. ValidateAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.validateadditionaldata(v=vs.111).aspx)* vrátila *hodnotu false*.

V zařízeních proti sadě anti-XSRF může také probíhat další kontrola během generování nebo ověřování tokenu a selhání během těchto kontrol může způsobit vyvolání výjimek. Další informace najdete v částech [WIF/ACS/ověřování založené na deklaracích](#_WIF_ACS) a možnosti **[Konfigurace a rozšiřitelnost](#_Configuration_and_extensibility)** .

<a id="_Scenarios_with_special"></a>

## <a name="scenarios-with-special-support"></a>Scénáře se zvláštní podporou

### <a name="anonymous-authentication"></a>Anonymní ověření

Systém Anti-XSRF obsahuje speciální podporu pro anonymní uživatele, kde "anonymní" je definováno jako uživatel, kde vlastnost *IIdentity. Authenticated* vrátí *hodnotu false*. Mezi scénáře patří poskytnutí ochrany XSRF na přihlašovací stránku (před ověřením uživatele) a vlastní schémata ověřování, kde aplikace používá jiný mechanismus než *IIdentity* k identifikaci uživatelů.

Pro podporu těchto scénářů odvoláte, že tokeny relace a pole jsou spojeny tokenem zabezpečení, což je 128 náhodně generovaný neprůhledný identifikátor. Tento token zabezpečení se používá ke sledování relace jednotlivých uživatelů při navigaci na webu, takže efektivně zachovává účel anonymního identifikátoru. Místo uživatelského jména se používá prázdný řetězec pro rutiny generace a ověřování popsané výše.

<a id="_WIF_ACS"></a>

### <a name="wif--acs--claims-based-authentication"></a>WIF/ACS/ověřování založené na deklaracích

Třídy *IIdentity* integrované do .NET Framework mají obvykle vlastnost, která *IIdentity.Name* postačuje k jednoznačné identifikaci konkrétního uživatele v rámci konkrétní aplikace. *FormsIdentity.Name* například vrátí uživatelské jméno uložené v databázi členství (což je jedinečné pro všechny aplikace v závislosti na dané databázi), *WindowsIdentity.Name* vrátí identitu uživatele kvalifikovanou doménou a tak dále. Tyto systémy neposkytují pouze ověřování. také *identifikují* uživatele k aplikaci.

Ověřování založené na deklaracích na druhé straně nemusí nutně vyžadovat určení konkrétního uživatele. Místo toho jsou typy *ClaimsPrincipal* a *hodnota ClaimsIdentity* přidružené k sadě instancí *deklarací* , kde jednotlivé deklarace identity můžou být 18 + roky stáří nebo je správce, aby cokoli jiného. Vzhledem k tomu, že uživatel není nezbytně identifikovaný, modul runtime nemůže pro tohoto konkrétního uživatele použít vlastnost *ClaimsIdentity.Name* jako jedinečný identifikátor. Tým viděli reálné příklady, kde *ClaimsIdentity.Name* vrací *hodnotu null*, vrátí popisný název (zobrazení) nebo jinak vrátí řetězec, který není vhodný pro použití jako jedinečný identifikátor pro uživatele.

Mnohé z nasazení, které používají ověřování založené na deklaracích, používá službu [Azure Access Control Service](https://msdn.microsoft.com/library/windowsazure/gg429786.aspx) (ACS), zejména. Služba ACS umožňuje vývojářům nakonfigurovat jednotlivé *zprostředkovatele identity* (například ADFS, poskytovatele účtu Microsoft, poskytovatele OpenID, jako je Yahoo! atd.), a poskytovatele identity vrátí *identifikátory názvů*. Tyto identifikátory názvů můžou obsahovat osobní údaje (PII), jako je e-mailová adresa, nebo by se daly jednat o anonymní osobní identifikátor (PPID). Řazená kolekce členů (poskytovatel identity, identifikátor názvu) dostatečně slouží jako vhodný sledovací token pro konkrétního uživatele při procházení lokality, takže modul runtime webového zásobníku ASP.NET může použít řazenou kolekci členů místo uživatelského jména při generování a ověřují se tokeny pole anti-XSRF. Konkrétní identifikátory URI pro poskytovatele identity a identifikátor názvu jsou:

- `http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider`
- `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`

(Další informace najdete na této [stránce s dokumentem ACS](https://msdn.microsoft.com/library/windowsazure/gg185971.aspx) .)

Při generování nebo ověřování tokenu bude modul runtime ASP.NET webového zásobníku za běhu vyzkoušet vazbu na tyto typy:

- `Microsoft.IdentityModel.Claims.IClaimsIdentity, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35` (pro sadu SDK pro WIF)
- `System.Security.Claims.ClaimsIdentity` (pro .NET 4,5).

Pokud existují tyto typy, a pokud *IIIIdentity* aktuálního uživatele implementuje nebo podtřídí jeden z těchto typů, bude zařízení anti-XSRF při generování a ověřování tokenů používat řazenou kolekci členů (poskytovatel identity, identifikátor názvu) místo uživatelského jména. Pokud žádná taková řazená kolekce členů není k dispozici, požadavek selže s chybou, která popisuje vývojáře postup konfigurace systému anti-XSRF pro pochopení konkrétního mechanismu ověřování založeného na deklaracích, který se používá. Další informace najdete v části **[Konfigurace a rozšiřitelnost](#_Configuration_and_extensibility)** .

### <a name="oauth--openid-authentication"></a>Ověřování OAuth/OpenID

V konečném případě má zařízení anti-XSRF zvláštní podporu pro aplikace, které používají ověřování OAuth nebo OpenID. Tato podpora je založená na heuristikě: Pokud aktuální *IIdentity.Name* začíná na http://nebo https://, pak se porovnávání uživatelského jména provede pomocí ordinálního porovnávání namísto výchozí porovnávací metody OrdinalIgnoreCase.

<a id="_Configuration_and_extensibility"></a>

## <a name="configuration-and-extensibility"></a>Konfigurace a rozšiřitelnost

V některých případech mohou vývojáři chtít mít užší kontrolu nad chováním generování a ověřování proti více XSRF. Může se třeba stát, že MVC a webové stránky budou automaticky přidávat soubory cookie HTTP do odpovědi nežádoucí a vývojáři si můžou chtít tyto tokeny uchovat jinde. Existují dvě rozhraní API pro pomoc s tímto:

`AntiForgery.GetTokens(string oldCookieToken, out string newCookieToken, out string formToken);`  
`AntiForgery.Validate(string cookieToken, string formToken);`

Metoda *Gettokens* přijímá jako vstup existující token relace ověření žádosti XSRF (který může být null) a vytváří jako výstup nový token relace ověření žádosti XSRF a token pole. Tokeny jsou jednoduše neprůhledné řetězce bez dekorace; hodnota *formToken* bude pro instanci nezabalená do &lt;vstupní&gt; značce. Hodnota *newCookieToken* může být null. Pokud k tomu dojde, hodnota *oldCookieToken* je stále platná a není nutné nastavit žádné nové soubory cookie odpovědi. Volající *Gettokens* zodpovídá za uchování všech potřebných souborů cookie odpovědí nebo pro vytváření potřebných značek. Samotná metoda *Gettokens* nemění odpověď v podobě vedlejšího efektu. Metoda *Validate* vezme příchozí tokeny relace a pole a spustí výše uvedenou logiku ověřování.

### <a name="antiforgeryconfig"></a>AntiForgeryConfig

Vývojář může nakonfigurovat systém Anti-XSRF z aplikace\_Start. Konfigurace je programová. Vlastnosti statického typu *AntiForgeryConfig* jsou popsány níže. Většina uživatelů, kteří používají deklarace identity, bude chtít nastavit vlastnost UniqueClaimTypeIdentifier.

| **Majetek** | **Popis** |
| --- | --- |
| **AdditionalDataProvider** | [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) , který poskytuje další data během generování tokenu a spotřebovává další data během ověřování tokenu. Výchozí hodnota je *null*. Další informace najdete v části [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) . |
| **Vlastnost CookieName** | Řetězec, který poskytuje název souboru cookie protokolu HTTP, který se používá k uložení tokenu relace anti-XSRF. Pokud tato hodnota není nastavená, automaticky se vygeneruje název založený na nasazené virtuální cestě aplikace. Výchozí hodnota je *null*. |
| **Vlastnost requireSSL** | Logická hodnota, která určuje, zda jsou tokeny anti-XSRF požadovány k odeslání přes kanál zabezpečený protokolem SSL. Pokud je tato hodnota *true*, všechny automaticky generované soubory cookie budou mít nastaven příznak "Secure" a rozhraní API pro anti-XSRF, pokud se volá z požadavku, který není odeslán přes protokol SSL. Výchozí hodnota je *false (NEPRAVDA*). |
| **SuppressIdentityHeuristicChecks** | Logická hodnota, která určuje, zda má systém Anti-XSRF deaktivovat podporu identit založených na deklaracích identity. Pokud je tato hodnota *true*, systém předpokládá, že *IIdentity.Name* je vhodný pro použití jako jedinečný identifikátor podle uživatele a nepokusí se o zvláštní případ *IClaimsIdentity* nebo *ClClaimsIdentity* , jak je popsáno v [WIF/ACS/ oddíl ověřování na základě deklarací](#_WIF_ACS) . Výchozí hodnota je `false`. |
| **UniqueClaimTypeIdentifier** | Řetězec, který označuje typ deklarace identity, který je vhodný pro použití jako jedinečný identifikátor podle uživatele. Pokud je tato hodnota nastavena a aktuální *IIdentity* je založená na deklaracích identity, systém se pokusí extrahovat deklaraci identity typu určenou parametrem *UniqueClaimTypeIdentifier*a odpovídající hodnota bude použita místo uživatelského jména uživatele, když generuje se token pole. Pokud se typ deklarace identity nenalezne, požadavek na systém se nezdaří. Výchozí hodnota je *null*, což znamená, že systém by měl použít řazenou kolekci členů (poskytovatel identity, identifikátor názvu), jak je popsáno výše v části místo uživatelského jména uživatele. |

<a id="_IAntiForgeryAdditionalDataProvider"></a>

### <a name="iantiforgeryadditionaldataprovider"></a>IAntiForgeryAdditionalDataProvider

Typ *[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)* umožňuje vývojářům roztáhnout chování systému anti-XSRF tím, že v každém tokenu Trip další data. Metoda *GetAdditionalData* je volána při každém vygenerování tokenu pole a návratová hodnota je vložena do vygenerovaného tokenu. Implementátor může vracet časové razítko, hodnotu NONCE nebo jakoukoli jinou hodnotu, kterou si z této metody přeje.

Podobně metoda *ValidateAdditionalData* je volána při každém ověření tokenu pole a řetězec "další data", který byl vložen v rámci tokenu, je předán metodě. Rutina ověřování by mohla implementovat časový limit (kontrolou aktuálního času v čase, který byl uložen při vytvoření tokenu), rutiny kontroly hodnoty nonce nebo libovolné jiné požadované logiky.

## <a name="design-decisions-and-security-considerations"></a>Rozhodnutí o návrhu a aspekty zabezpečení

Token zabezpečení, který odkazuje na tokeny relace a pole, je technicky nutný jenom při pokusu o ochranu anonymních nebo neověřených uživatelů proti útokům na XSRF. Při ověření uživatele se dá samotný ověřovací token (předpokládaný ve formě souboru cookie) použít jako jednu polovinu páru tokenů synchronizátoru. Existují však platné scénáře ochrany přihlašovacích stránek, ke kterým přirazí neověření uživatelé, a logika anti-XSRF byla jednodušší, protože vždy generuje a ověřuje token zabezpečení, a to i pro ověřené uživatele. Také poskytuje dodatečnou ochranu v případě, že útočník může v případě ohrožení zabezpečení v případě, že je nastavení nebo odhad tokenu relace jinou prahovou hodnotu, aby mohl útočník překonat.

Vývojáři by měli při hostování více aplikací v jedné doméně používat upozornění. Například i když jsou *example1.cloudapp.NET* a *example2.cloudapp.NET* různými hostiteli, existuje implicitní vztah důvěryhodnosti mezi všemi hostiteli v doméně *\*. cloudapp.NET* . Tento implicitní vztah důvěryhodnosti [umožňuje potenciálním nedůvěryhodným hostitelům ovlivnit soubory cookie ostatních souborů](http://stackoverflow.com/questions/9636857/how-can-asp-net-or-asp-net-mvc-be-protected-from-related-domain-cookie-attacks) (zásady stejného původu, které řídí požadavky AJAX, nemusí nutně platit pro soubory cookie http). Modul runtime webového zásobníku ASP.NET je v tom, že uživatelské jméno je vložené do tokenu pole, takže i v případě, že škodlivá subdoména může přepsat token relace, nebude pro uživatele možné vygenerovat platný token pole. Pokud se ale v takovém prostředí hostuje, předdefinovaná rutina anti-XSRF se pořád nemůže chránit proti zneužití relace nebo k přihlášení XSRF.

Rutiny anti-XSRF momentálně nebrání proti [clickjacking](https://www.owasp.org/index.php/Clickjacking). Aplikace, které se chtějí chránit proti clickjacking, můžou snadno učinit tak, že se každou odpověď pošle hlavičkou možností X-frame: SAMEORIGIN. Tato hlavička je podporovaná všemi nedávnými prohlížeči. Další informace najdete na blogu k [internetovým](https://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx)odkazům, na [blogu SDL](https://blogs.msdn.com/b/sdl/archive/2009/02/05/clickjacking-defense-in-ie8.aspx)a v [OWASP](https://www.owasp.org/index.php/Clickjacking). Modul runtime webového zásobníku ASP.NET může v některých budoucích vydáních vytvořit tuto hlavičku automaticky pomocníkům pro usnadnění a webové stránky, aby se aplikace automaticky chránily proti tomuto útoku.

Vývojáři webu by měli pokračovat v zajištění, že jejich lokalita není zranitelná vůči útokům XSS. Útoky XSS jsou velmi výkonné a při úspěšném zneužití by došlo také k přerušení ochrany modulu runtime webového zásobníku ASP.NET proti útokům XSRF.

## <a name="acknowledgment"></a>Potvrzení

[@LeviBroderick](https://twitter.com/LeviBroderick), který napsal mnoho z bezpečnostních kódů ASP.NET, tyto informace jsou hromadné.
